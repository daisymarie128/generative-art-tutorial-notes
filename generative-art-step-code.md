## STEP 1:

### Lets just draw a line
```js
  ctx.beginPath();
  ctx.moveTo(0, 0);
  ctx.lineTo(height, width);
  ctx.stroke();
```


## STEP 2:

### Lets start drawing multiple tiles
```js

for (let y = 0; y <= (height / tileSize); y++) {
  for (let x = 0; x <= (width / tileSize); x++) {
    ctx.beginPath();
    ctx.moveTo(0, 0);
    ctx.lineTo(height, width);
    ctx.stroke();
  }
}
```


## STEP 3:

### Re-adjust code to work with tiles:
```js

for (let y = 0; y <= (height / tileSize); y++) {
  for (let x = 0; x <= (width / tileSize); x++) {
    const xOffset = x * tileSize;
    const yOffset = y * tileSize;

    ctx.beginPath();
    ctx.moveTo(xOffset, yOffset);
    ctx.lineTo(xOffset + tileSize, yOffset + tileSize);
    ctx.stroke();
  }
}
```

## STEP 4:

### Write some logic to change direction:
```js

for (let y = 0; y <= (height / tileSize); y++) {
  for (let x = 0; x <= (width / tileSize); x++) {
    const xOffset = x * tileSize;
    const yOffset = y * tileSize;

    ctx.beginPath();
    ctx.moveTo(xOffset, yOffset);
    ctx.lineTo(xOffset + tileSize, yOffset + tileSize);
    ctx.stroke();

    if (leftToRight) {
      // draw  right to left line = \
    } else {
      // draw  left to right line = /
    }
  }
}
```

```js

for (let y = 0; y <= (height / tileSize); y++) {
  for (let x = 0; x <= (width / tileSize); x++) {
    const leftToRight = true;
    const xOffset = x * tileSize;
    const yOffset = y * tileSize;

    if (leftToRight) {
      // draw  right to left line = \
      ctx.moveTo(xOffset, yOffset);
      ctx.lineTo(xOffset + tileSize, yOffset + tileSize);
    } else {
      // draw  left to right line = /
      ctx.moveTo(xOffset + tileSize, yOffset);
      ctx.lineTo(xOffset, yOffset + tileSize);
    }

    ctx.stroke();
  }
}
```

## STEP 5:

### Next lets make our canvas clear itself:
```js
function generateLines(ctx, tileSize, width, height){
  ctx.clearRect(0, 0, width, height);
  
  for (let y = 0; y <= (height / tileSize); y++) {
    for (let x = 0; x <= (width / tileSize); x++) {
      const leftToRight = Math.random() >= .5;
      const xOffset = x * tileSize;
      const yOffset = y * tileSize;

      ctx.beginPath();
      
      if (leftToRight) {
        // draw  right to left line = \
        ctx.moveTo(xOffset, yOffset);
        ctx.lineTo(xOffset + tileSize, yOffset + tileSize);
      } else {
        // draw  left to right line = /
        ctx.moveTo(xOffset + tileSize, yOffset);
        ctx.lineTo(xOffset, yOffset + tileSize);
      }
      
      ctx.stroke();
    }
  }
}
```

## STEP 6:

### Randomise the color:
```js
function generateLines(ctx, tileSize, width, height){
  ctx.clearRect(0, 0, width, height);
  
  for (let y = 0; y <= (height / tileSize); y++) {
    for (let x = 0; x <= (width / tileSize); x++) {
      const leftToRight = Math.random() >= .5;
      const xOffset = x * tileSize;
      const yOffset = y * tileSize;

      ctx.beginPath();
      ctx.strokeStyle = `rgb(0,
                    ${Math.floor(255 - (y * 10))}, 
                    ${Math.floor(255 - (x * 10))})`;
      if (leftToRight) {
        // draw  right to left line = \
        ctx.moveTo(xOffset, yOffset);
        ctx.lineTo(xOffset + tileSize, yOffset + tileSize);
      } else {
        // draw  left to right line = /
        ctx.moveTo(xOffset + tileSize, yOffset);
        ctx.lineTo(xOffset, yOffset + tileSize);
      }
      
      ctx.stroke();
    }
  }
}
```