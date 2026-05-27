# Ex05 Image Carousel
## Date:27.05.2026

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
App.js
```
import React, { useState, useEffect } from "react";
import "./App.css";

const images = [
  "https://picsum.photos/id/1015/800/400",
  "https://picsum.photos/id/1016/800/400",
  "https://picsum.photos/id/1018/800/400",
];

function App() {
  const [current, setCurrent] = useState(0);

  // Next Slide
  const nextSlide = () => {
    setCurrent((prev) => (prev + 1) % images.length);
  };

  // Previous Slide
  const prevSlide = () => {
    setCurrent((prev) =>
      prev === 0 ? images.length - 1 : prev - 1
    );
  };

  // Auto Slide
  useEffect(() => {
    const interval = setInterval(() => {
      nextSlide();
    }, 3000);

    return () => clearInterval(interval);
  }, []);

  return (
    <div className="carousel">
      <h1>React Image Carousel</h1>

      <div className="slider">
        <button className="btn" onClick={prevSlide}>
          ❮
        </button>

        <img
          src={images[current]}
          alt="slide"
          className="image"
        />

        <button className="btn" onClick={nextSlide}>
          ❯
        </button>
      </div>

      <div className="dots">
        {images.map((_, index) => (
          <span
            key={index}
            className={current === index ? "dot active" : "dot"}
            onClick={() => setCurrent(index)}
          ></span>
        ))}
      </div>
    </div>
  );
}

export default App;
```
App.css
```
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f4f4;
}

.carousel {
  text-align: center;
  margin-top: 40px;
}

.slider {
  position: relative;
  width: 80%;
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

.image {
  width: 100%;
  max-width: 800px;
  height: 400px;
  object-fit: cover;
  border-radius: 10px;
}

.btn {
  position: absolute;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  font-size: 30px;
  padding: 10px 15px;
  cursor: pointer;
  border-radius: 50%;
  z-index: 1;
}

.btn:first-of-type {
  left: 20px;
}

.btn:last-of-type {
  right: 20px;
}

.dots {
  margin-top: 15px;
}

.dot {
  height: 15px;
  width: 15px;
  margin: 0 5px;
  display: inline-block;
  border-radius: 50%;
  background: gray;
  cursor: pointer;
}

.active {
  background: #3498db;
}
```
Index.js
```
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```


## OUTPUT
<img width="1911" height="954" alt="Screenshot 2026-05-27 085053" src="https://github.com/user-attachments/assets/c8644ad2-476f-4a24-89e3-b399c6236735" />



## RESULT
The program for creating Image Carousel using React is executed successfully.
