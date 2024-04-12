<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Webpage</title>
<style>
  /* Ensure the page fills the viewport */
  body, html {
    height: 100%;
    width: 100%;
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
    animation: fadeIn 1s ease-in-out forwards; /* Fade-in effect */
    overflow: hidden; /* Hide page scrollbars */
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  .fullscreen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: url('https://p.sda1.dev/16/7931111adc8303a50ee9073dedd8f826/截屏2024-04-09 10.17.06.png') no-repeat center center;
    background-size: contain; /* Ensure background image fully covers and maintains aspect ratio */
    color: #fff;
    font-size: 2em;
    cursor: pointer;
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  /* Display as orange bar on mobile devices */
  @media (max-width: 768px) {
    .fullscreen {
      background: url('https://p.sda1.dev/16/74e1ebabfebf7a8b4388e4608d071a16/截屏2024-04-11 13.11.58.png') no-repeat center center;
      background-size: contain; /* Ensure background image fully covers and maintains aspect ratio */
    }
  }

  .gridLayout {
    display: none;
    width: 100%;
    height: 100%;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    gap: 0;
    padding: 10px;
    box-sizing: border-box;
    background: #ddd;
  }

  .gridLayout.show {
    display: grid;
  }

  .gridItem {
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 100%;
    position: relative;
    cursor: pointer;
  }

  .subGridItem {
    background: #bbb;
    width: 33.33%;
    height: 100%;
    border-right: 2px solid #fff;
  }

  .subGridItem.right {
    width: 66.66%;
    background: url('https://p.sda1.dev/16/74e1ebabfebf7a8b4388e4608d071a16/截屏2024-04-11 13.11.58.png') no-repeat center center;
    background-size: cover;
  }

  .videoItem {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .videoItem video {
    min-width: 100%;
    min-height: 100%;
  }

  /* Ensure the first page remains at 100% scale when resizing the browser */
  #welcomeScreen > div {
    max-width: 100vw;
    max-height: 100vh;
  }
</style>
</head>
<body>

<div id="welcomeScreen" class="fullscreen">
  <div></div>
</div>

<div id="gridLayout" class="gridLayout">
  <div class="gridItem" style="background: url('https://p.sda1.dev/16/7931111adc8303a50ee9073dedd8f826/截屏2024-04-09 10.17.06.png') no-repeat center center; background-size: contain;" onclick="window.location.href='file:///Users/taianqi/Desktop/9.html';"></div>
</div>

<div id="thirdPage" style="display:none;">
  <div>Content of the third page</div>
</div>

<script>
  var welcomeScreen = document.getElementById('welcomeScreen');
  var gridLayout = document.getElementById('gridLayout');
  var thirdPage = document.getElementById('thirdPage');

  welcomeScreen.addEventListener('click', function() {
    this.style.display = 'none';
    gridLayout.classList.add('show');
    thirdPage.style.display = 'block'; // Display the content of the third page

    // Clear other modules except the initial one to avoid duplication
    while(gridLayout.children.length > 1) {
      gridLayout.removeChild(gridLayout.lastChild);
    }

    // Dynamically generate 7 other modules, preserving 2 video module positions
    for (var i = 0; i < 7; i++) {
      var gridItem = document.createElement('div');
      gridItem.className = 'gridItem';
      gridLayout.appendChild(gridItem);

      if (i === 4) {
        // Add central three vertical bars
        for (var j = 0; j < 3; j++) {
          var subGridItem = document.createElement('div');
          subGridItem.className = 'subGridItem';
          if(j === 2) { // Change to orange bar only when j=2, meeting the special requirements on mobile devices
            subGridItem.classList.add('right'); // Add special style for the last one
          }
          subGridItem.setAttribute("onclick", "window.location.href='./page" + (i + j + 1) + ".html';"); // Change here to set the webpage link for each vertical bar
          gridItem.appendChild(subGridItem);
        }
      } else {
        // Add five vertical bars
        for (var k = 0; k < 5; k++) {
          var subGridItemDefault = document.createElement('div');
          subGridItemDefault.className = 'subGridItem';
          subGridItemDefault.setAttribute("onclick", "window.location.href='./page" + (i + k + 1) + ".html';"); // Change here to set the webpage link for each vertical bar
          gridItem.appendChild(subGridItemDefault);
        }
      }
    }

    // Add the first video module to the bottom left corner
    var firstVideoItem = document.createElement('div');
    firstVideoItem.className = 'gridItem videoItem';
    firstVideoItem.innerHTML = '<video src="your-first-video-url.mp4" controls></video>';
    gridLayout.insertBefore(firstVideoItem, gridLayout.children[6]); // At the 7th position, bottom left corner

    // Add the second video module to the first row third module position
    var secondVideoItem = document.createElement('div');
    secondVideoItem.className = 'gridItem videoItem';
    secondVideoItem.innerHTML = '<video src="your-second-video-url.mp4" controls></video>';
    var gridItemToReplace = gridLayout.children[2];
    gridLayout.insertBefore(secondVideoItem, gridItemToReplace);
    gridLayout.removeChild(gridItemToReplace);
  });
</script>

</body>
</html>
