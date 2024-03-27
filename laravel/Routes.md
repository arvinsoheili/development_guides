# Routes

### Named Routes

1.  go to your route file and find your target route.
2.  type `->name('route name');` at the end of your route.
3.  now you can use your prefered name in your `a` tags like below:
```
<a href='{{ route('route name')}}></a>

```
NOTE: if you got a wildcard in your route you should type it like `, $var-you-passed-in-view->id`
