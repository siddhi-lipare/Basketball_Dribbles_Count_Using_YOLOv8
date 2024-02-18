# Basketball_Dribbles_Count_Using_YOLO
Analysing various parameters for a given basketball dribble video: Dribble count, Ball velocity, Dribble frequency

----------
*Prerequisites*
-------------
- `Python 3.10` 
- Install necessary packages using the following command:
```bash
pip install -r requirements.txt
````

*Documentation*
-------------
- Run the `dribble-count.ipynb` file.

- The video displays the Dribble Count, Ball Velocity and Dribble Frequency.
- The video output has been saved as `outputvid.mp4`

*How I Approached the solution*
-------------
- In the [Vacant-Seat-Detection-in-Restaurants](https://github.com/siddhi-lipare/Vacant-Seat-Detection-in-Restaurants) repo I previously worked on, I had used YOLOv8 for object detection. Similarly, the basketball in the video has been detected using YOLOv8 (COCO Label 'sports ball').
  
#### For counting the number of dribbles:
- I simply measured the distance of the ball every 5 frames whenever the ball moves in the downward direction (when y-coordinate is decreasing) using the x,y,z coordinates since I saved the ball position corresponding to the timestamps in a cvs file `csv/dribble_data.csv`.
- The distance here is simply `y_distance = current_y - previous_y` since we don't need to consider the x and z coordinates for now.
-  If the `y_distance` is greater than a threshold (70 after checking the distance from height to ground), then dribble count increases by 1.
-  Upward movement of ball wasn't considered since a dribble is incremented by 1 only when the ball reaches back to each original position.

#### For calculating the Ball Velocity:

$$
Ball Velocity = \frac{Distance}{Time}
$$


Where Euclidean Distance (norm) and the Time difference between every 5 frames is considered.

#### For calculating the Dribble Frequency:
$$
Dribble Frequency = \frac{Dribble Count}{Time}
$$

Thus we know the number of dribbles per seconds that has been done.
