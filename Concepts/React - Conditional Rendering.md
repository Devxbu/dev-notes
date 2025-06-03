Conditional rendering in React dynamically renders components based on specific conditions. This is something we encounter quite a lot in our daily life when we browse the internet. For example, when you subscribe to a youtube channel, the subscribe button takes on a different design, this is entirely due to conditional rendering. There are 2 different ways of conditional rendering (if else statement and tenary). First let's write an example with if else statements

```jsx
function sub() {
	const [isSub, setIsSub] = useState(false);
	const subscribe = () => {setIsSub(!isSub)};

	var btn;
	var btn_color;

	if (isSub) {
		btn = "Subscribed";
		btn_color = "blue";
	} else {
		btn = "Subscribe";
		btn_color = "red";
	}

	return (
		<button 
			onClick={subscribe}
			style={{
				backgroundColor: btn_color
			}}
		>
		{btn}
		</button>
	);
};
```

If else statements made the code unnecessarily much longer. Let's try the same thing with a tenary statement instead

```jsx
function sub() {
	const [isSub, setIsSub] = useState(false);
	const subscribe = () => {setIsSub(!isSub)};
	
	var btn = isSub ? "Subscribed" : "Subscribe";
	var btn_color = isSub ? "blue" : "red";
	
	return (
		<button 
			onClick={subscribe}
			style={{
				backgroundColor: btn_color
			}}
		>
		{btn}
		</button>
	);
};
```

In this way, our code has become shorter and more eye-catching while performing the same operation. In this way, we have rendered in a dynamic way