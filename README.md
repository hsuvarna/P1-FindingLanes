# P1-FindingLanes
Python project to find the lanes on the road
1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
  First convert the color image of the road to gray scale image. This allows us to view all areas of the image uniformly i.e. we removed the color separations. But we still have gray scale b/w  variations.
2. Then smoothed the image using gaussian filter. Smoothing makes the road markers take out rough edges.
3. Detect the edges using canny() method of OpenCV. The edges are key to marking the road boundaries. But we can get edges of other objects also in the picture.
4. In order to filter out the edges of other objects, define a region of interest. This being the area of the road lanes which is in the center of the image. Then mask these edges with 255 and mask edges out side this region as zeros.
5. Now we have region of interest and edges. Out of them, only some represent he lanes. The lane characteristic being  set of 2-paralell lines. The two lines can further be thick representing the edges. Running hough transform on the edges detected in step 7 finds lane lines only. Hough transform helps us compute the lines easily in rho-theta space. m-b space has infinity slope problem (division by 0).rho-theta eliminates that. Here parallel lines become dots in vertical line in mb space. Dots on the road lane line become intersecting sin curves. The bunch of vertical intersection points can tell the x,y of lane lines.
6. The weighted function can then distinguish the lane lines on top of the original image.
7. I chose the -ve slope and + slope to identify the left line and right line of a lane. Then I computed the avreage slope of all left and right lanes. Using average slopes I extrapolated the (x_max, y_min) for left and right lines. This allowed me to draw the road lanes across the height of the image. Also while drawing, I joined the lane segments by always maintaing the previous line segment in the loop. I will join current and previous line segments.


# Identify potential shortcomings with your current pipeline
1. The sign of slope is almost a pretty good indicator to separate left vs right lanes but it can pose problem for straight lines.
2. If road lane markings are wiped by rain, I dont know what kind of results I get.
3. Spurious line segments here and there draw lines across lanes.

# Suggest possible improvements to your pipeline
1. Handle different types of images. grayscale() only takes care of rgb images.
2. draw_lines() can have more heuristics in identifying left vs right line segments.
3. sometimes the lane upper lines are not drawn equal height on left vs right border of the line.
