# Ex05 Image Carousel
## Date:15.10.2025

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
### Home.jsx
```
import React, { useState, useEffect } from "react";

export default function Home() {
  const images = [
    "https://picsum.photos/id/1018/800/400",
    "https://picsum.photos/id/1015/800/400",
    "https://picsum.photos/id/1019/800/400",
    "https://picsum.photos/id/1021/800/400"
  ];

  const [current, setCurrent] = useState(0);

  // Auto-slide every 3 seconds
  useEffect(() => {
    const timer = setInterval(() => {
      setCurrent((prev) => (prev + 1) % images.length);
    }, 3000);
    return () => clearInterval(timer);
  }, [images.length]);

  // Manual navigation
  const nextSlide = () => setCurrent((prev) => (prev + 1) % images.length);
  const prevSlide = () => setCurrent((prev) => (prev - 1 + images.length) % images.length);

  return (
    <div style={styles.carousel}>
      <button style={styles.btn} onClick={prevSlide}>❮</button>
      <img src={images[current]} alt="carousel" style={styles.image} />
      <button style={styles.btn} onClick={nextSlide}>❯</button>
      <div style={styles.dots}>
        {images.map((_, i) => (
          <span
            key={i}
            onClick={() => setCurrent(i)}
            style={{
              ...styles.dot,
              backgroundColor: current === i ? "#333" : "#bbb"
            }}
          />
        ))}
      </div>
    </div>
  );
}

const styles = {
  carousel: {
    
    position: "relative",
    width: "800px",
    height: "400px",
    margin: "auto",
    overflow: "hidden",
    borderRadius: "12px",
    boxShadow: "0 4px 12px rgba(0,0,0,0.3)"
  },
  image: {
    width: "100%",
    height: "100%",
    objectFit: "cover",
    borderRadius: "12px",
    transition: "opacity 0.5s ease-in-out"
  },
  btn: {
    position: "absolute",
    top: "50%",
    transform: "translateY(-50%)",
    backgroundColor: "rgba(255,255,255,0.6)",
    border: "none",
    fontSize: "2rem",
    cursor: "pointer",
    zIndex: 2,
    padding: "0 12px",
    borderRadius: "50%"
  },
  dots: {
    position: "absolute",
    bottom: "12px",
    width: "100%",
    textAlign: "center"
  },
  dot: {
    display: "inline-block",
    width: "12px",
    height: "12px",
    borderRadius: "50%",
    margin: "0 4px",
    cursor: "pointer"
  }
};

```
### App.jsx
```
import React from "react";
import Home from "./Home.jsx";

function App() {

  return (
    <div style={styles.wrapper}>
      <div style={styles.content}>
        <h1 style={styles.heading}>React Image Carousel</h1>
        <Home />
      </div>
    </div>
    
  );
}
const styles = {
  wrapper: {
    display: "flex",
    justifyContent: "center",  // horizontal center
    alignItems: "center",      // vertical center
    height: "100vh",           // full viewport height
    width: "100vw",            // full viewport width
    backgroundColor: "#252222ff", // optional background
  },
  content: {
    textAlign: "center",
  },
  heading: {
    marginBottom: "20px",
  }
};
export default App
```
## OUTPUT
<img width="1562" height="824" alt="image" src="https://github.com/user-attachments/assets/9efd018a-d438-4ed7-9a86-dc1c7acd3f2a" />
<img width="1198" height="743" alt="image" src="https://github.com/user-attachments/assets/1a40da0d-390f-4bc9-9d06-85f9edec91d5" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
