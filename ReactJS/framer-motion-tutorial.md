# Framer Motion Tutorial Transcript

Animations are increasingly becoming more and more popular on websites, allowing us to get a bit more creative with how we build and design our sites. Animations can be used to tell a story or convey the personality of a brand, making websites more memorable and engaging.

## Getting Started

We have a few libraries that help us to animate with ReactJS, such as:
- GSAP
- React Spring
- **Framer Motion** (focus of this tutorial)

We’ll also use:
- **Tailwind CSS** (for design)
- **Vite** (for project setup)

> **Note**: This video is not sponsored.

## Project Setup

1. Create your React project using Vite.
2. Install Tailwind CSS (optional, but used in this tutorial).
3. Clear `App.jsx` and return an empty `<div>` with a `<section>` inside.
4. In `index.css`, make sure Tailwind’s `base`, `components`, and `utilities` are included.
5. Set a global background: `bg-slate-950`.

## Installing Framer Motion

Use the install command from Framer Motion’s website:
```bash
npm install framer-motion
```

## Initial Layout

Set up a 2x3 grid for 6 animations. Example section styles:
```jsx
<section className="grid grid-cols-3 p-10 gap-10">
  <div className="bg-slate-800 aspect-square rounded-lg justify-center flex items-center gap-10"></div>
  <!-- Repeat 5 more times -->
</section>
```

## Animation 1: Staggered Fade-in Grid

- Import `motion` from `framer-motion`
- Wrap section and inner divs with `motion`
- Use `variants` for staggered animations:
```js
const gridContainerVariants = {
  hidden: { opacity: 0 },
  show: {
    opacity: 1,
    transition: { staggerChildren: 0.25 },
  },
};

const gridSquareVariants = {
  hidden: { opacity: 0 },
  show: { opacity: 1 },
};
```

Apply with:
```jsx
<motion.section variants={gridContainerVariants} initial="hidden" animate="show">
  <motion.div variants={gridSquareVariants} />
</motion.section>
```

## Animation 2: Fade & Y-axis Movement

Use `initial` and `animate` props directly:
```jsx
<motion.div initial={{ opacity: 0, y: 100 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 1, ease: "easeOut", delay: 0.2 }} />
<motion.div initial={{ opacity: 0, y: -100 }} animate={{ opacity: 1, y: 0 }} transition={{ delay: 0.4 }} />
```

## Animation 3: Transform with Scale, Rotation, Border Radius

```jsx
<motion.div animate={{
  scale: [1, 2, 2, 1],
  rotate: [0, 90, 90, 0],
  borderRadius: ["10%", "10%", "50%", "10%"]
}}
transition={{
  duration: 5,
  ease: "easeInOut",
  repeat: Infinity,
  repeatDelay: 1,
}} />
```

Set `repeat: 2` if not infinite.

## Animation 4: Hover and Tap Button

```jsx
<motion.button
  whileTap={{ scale: 0.9 }}
  whileHover={{ scale: 1.1, backgroundColor: "#10b981", color: "#fff" }}
  transition={{ bounce: 0.4, damping: 10, stiffness: 600 }}
/>
```

## Animation 5: Draggable Square with Constraints

```jsx
<motion.div drag dragConstraints={{ top: -125, right: 125, bottom: 125, left: -125 }} dragTransition={{ bounceStiffness: 300, bounceDamping: 10 }} />
```

## Animation 6: Scroll Progress Indicator

```js
const { scrollYProgress } = useScroll();
<motion.div style={{ scaleY: scrollYProgress }} />
```

## Animation 7: Animated SVG Path (Lightning Bolt)

```js
const svgIconVariants = {
  hidden: { opacity: 0, pathLength: 0, fill: "rgba(255,255,0,0)" },
  visible: { opacity: 1, pathLength: 1, fill: "rgba(255,255,0,1)" },
};
```

```jsx
<motion.path
  variants={svgIconVariants}
  initial="hidden"
  animate="visible"
  transition={{
    fill: { duration: 2, ease: "easeIn", delay: 2, repeat: Infinity, repeatType: "reverse", repeatDelay: 1 },
    default: { duration: 2, ease: "easeInOut", delay: 1, repeat: Infinity, repeatType: "reverse", repeatDelay: 1 },
  }}
/>
```

## Animation 8: Scroll Into View & X-Axis Translation

```js
const containerRef = useRef();
const isInView = useInView(containerRef, { once: true });
const mainControls = useAnimation();

useEffect(() => {
  if (isInView) mainControls.start("visible");
}, [isInView]);
```

```jsx
<motion.h1
  ref={containerRef}
  initial="hidden"
  animate={mainControls}
  variants={{
    hidden: { opacity: 0, y: 75 },
    visible: { opacity: 1, y: 0 },
  }}
  transition={{ delay: 0.3 }}
/>
```

## Animation 9: Paragraph Scroll Transform

```js
const { scrollYProgress } = useScroll({ target: containerRef, offset: ["start end", "end end"] });
const x1 = useTransform(scrollYProgress, [0, 1], ["-100%", "0%"]);
const x2 = useTransform(scrollYProgress, [0, 1], ["100%", "0%"]);
```

```jsx
<motion.p style={{ translateX: x1 }} />
<motion.p style={{ translateX: x2 }} />
```

## Conclusion

Framer Motion can be a confusing library at first, but it offers powerful tools to bring your website to life. Be sure to explore the [Framer Motion docs](https://www.framer.com/motion/) and experiment with different animation types.

Stay healthy, stay safe, and happy coding!