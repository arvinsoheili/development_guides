# Syncing Laravel Logs with Discord Channel

### 1. create an webhook
- go to your desired discord channel
- go to channel settings -> integrations -> webhooks
- create new webhook and set the desired channel
- copy webhook by clicking on "Copy Webhook URL"

### 2. Install Guzzle HTTP Client:
if you don't have it installed yet, you can install it by this command:
```
composer require guzzlehttp/guzzle
```

### 3. Set Up Logging Configuration in Laravel:
- open `` config/logging.php`` file in you application
- locate ``stack`` in `Log Channels` and update it with this:
```
'stack' => [
            'driver' => 'stack',
            'channels' => ['single', 'discord'],
            'ignore_exceptions' => false,
        ],
```
- add new logging channel with this code:
```
 'discord' => [
        'driver' => 'custom',
        'via' => App\Logging\DiscordLogger::class,
        'level' => 'debug',
        'url' => env('DISCORD_WEBHOOK_URL'),
    ],
```

### 4. Create a Custom Logger:
#### 1. Update the CA Certificates on Your System

- Download the latest version of `cacert.pem` file from https://curl.se/docs/caextract.html
- Configure PHP to use this certificate bundle. Open your php.ini file and add or update the following line:
```
curl.cainfo = "C:\path\to\cacert.pem"
```
- Restart your web server or PHP service to apply the changes.

#### 2. Update the Guzzle Client to Use the CA Bundle

- Create a directory app/Logging if it doesn’t exist.
- Create a file DiscordLogger.php within this directory.
```
<?php
namespace App\Logging;

use Monolog\Logger;
use Monolog\Handler\AbstractProcessingHandler;
use Monolog\LogRecord;
use GuzzleHttp\Client;
use GuzzleHttp\Exception\RequestException;

class DiscordLogger
{
    public function __invoke(array $config)
    {
        $logger = new Logger('discord');

        $handler = new class($config['url']) extends AbstractProcessingHandler {
            protected $url;
            protected $client;

            public function __construct($url, $level = Logger::DEBUG, bool $bubble = true)
            {
                if (!is_string($url) || empty($url)) {
                    throw new \Exception('The URL must be a non-empty string. Current value: ' . var_export($url, true));
                }

                parent::__construct($level, $bubble);
                $this->url = $url;
                $this->client = new Client([
                    'verify' => 'path/to/cacert.pem' // replace with your .pem path.
                ]);
            }

            protected function write(LogRecord $record): void
            {
                try {
                    $this->client->post($this->url, [
                        'json' => [
                            'content' => $record->formatted,
                        ],
                    ]);
                } catch (RequestException $e) {
                    // Handle exception if necessary
                }
            }
        };

        $logger->pushHandler($handler);

        return $logger;
    }
}

```
### 5. Set Environment Variable:
Add your Discord webhook URL to the .env file:
```
DISCORD_WEBHOOK_URL=ADD_YOUR_DISCORD_WEBHOOK

```

