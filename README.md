# MWAD_EX05_image-carousel-in-react
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
### ImageCarousel.js:
```
import React, { useState, useEffect } from "react";
import "./ImageCarousel.css";

const ImageCarousel = ({ images }) => {
  // Step 2: State Management
  const [currentIndex, setCurrentIndex] = useState(0);

  // Step 3: Navigation Controls
  const nextImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex + 1) % images.length);
  };

  const prevImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex - 1 + images.length) % images.length);
  };

  // Step 5: Auto-Rotation
  useEffect(() => {
    const interval = setInterval(nextImage, 3000);
    return () => clearInterval(interval); // cleanup
  }, [images.length]);

  // Step 4: Displaying the Image
  return (
    <div className="carousel-container">
      <button onClick={prevImage} className="nav-button prev">❮</button>
      <img src={images[currentIndex]} alt="carousel" className="carousel-image" />
      <button onClick={nextImage} className="nav-button next">❯</button>
    </div>
  );
};

export default ImageCarousel;
```
### ImageCarousel.css:
```
.carousel-container {
  position: relative;
  width: 600px;
  height: 350px;
  margin: 40px auto;
  overflow: hidden;
  border-radius: 15px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.3);
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 15px;
}

.nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255,255,255,0.7);
  border: none;
  padding: 10px 15px;
  font-size: 24px;
  cursor: pointer;
  border-radius: 50%;
  transition: background 0.3s;
}

.nav-button:hover {
  background: rgba(255,255,255,1);
}

.prev {
  left: 15px;
}

.next {
  right: 15px;
}
```
### App.js:
```
import React from "react";
import ImageCarousel from "./components/ImageCarousel";

function App() {
  const images = [
    "https://picsum.photos/id/1018/600/350",
    "https://picsum.photos/id/1025/600/350",
    "https://picsum.photos/id/1037/600/350",
    "https://picsum.photos/id/1043/600/350",
  ];

  return (
    <div>
      <h1 style={{ textAlign: "center" }}>React Image Carousel</h1>
      <ImageCarousel images={images} />
    </div>
  );
}

export default App;
```
## OUTPUT
<img width="1422" height="890" alt="image" src="https://github.com/user-attachments/assets/9f9a5c03-1f58-4524-abb7-98adaee6265a" />
<img width="1445" height="868" alt="image" src="https://github.com/user-attachments/assets/d9196c1d-028b-4ca6-974a-82c25b566811" />
<img width="1222" height="735" alt="image" src="https://github.com/user-attachments/assets/e2f4a36c-6194-426d-aa72-4a97ad74ae25" />
<img width="1060" height="782" alt="image" src="https://github.com/user-attachments/assets/507b39f1-b434-422c-a468-23f49f6cf7a9" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
