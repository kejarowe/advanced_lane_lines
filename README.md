## Advanced Lane Lines Project
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

The purpose of this project is to develop a pipeline which can highlight the subject vehicle's lane in the [project_video.mp4](./project_video.mp4) provided as part of this project and generate a new video, which I called [output.mp4](./output.mp4). This project is similar to the first lane finding project (Project 1 in the SDC Nanodegree), but notable differences include:

* Highlighting the entire lane rather than just the left and right lane markers
* Robut lane detection in areas of changing pavement colors and shadows
* Calculation and display of lane curvature and vehicle lateral offset

To implement the pipeline, I took the following steps:

* Computed the camera calibration matrix and distortion coefficients using given a set of chessboard images.
* Apply the distortion correction to the raw image.  
* Use color transforms and gradients to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view"). 
* Detect left and right lane pixels individually and fit each to 2nd order polynomial.
* Use left and right polynomials to determine curvature of the lane and vehicle position with respect to center.
* If the polynimial fit returns a bad result, use fit from prior frame to improve result
* Smooth noisy curvature calculations using several frames worth of detections
* Warp a polygon which fills the detected lane boundaries back onto the original image.
* Print numerical estimation of lane curvature and vehicle position with respect to center in each frame.

Further details of my pipeline are included in [advanced_lane_lines.ipynb](./advanced_lane_lines.ipynb). Although this pipeline is fairly robust, there are aspects that could be improved. First, various thresholds are used throughout the pipeline which are handtuned to produce a good result on the [project_video.mp4](./project_video.mp4) input. An automated threshold selection method could almost certainly produce (at least slightly) better results. Second, tuning the thresholds on a larger dataset would further improve robustness. Third, in order to produce a smooth curvature value, several "raw curvature" values are used from past measurements/frames. If there is a sudden change in curvature, this method of filtering would lead to a delay in a reported value for "current curvature" which is representative of the actual value

Although this pipeline for lane marker detection is more robust than the pipeline in the first project, there are still situations in which it would likely fail. If there are tar strips on the road which cover a large percentage of the lane markers, that would present a major challenge for this pipeline. Heavily faded lane markers may also have lower saturation values which would effect the performance of this pipeline. Another particulary challenging situation would be running this pipeline in the rain. When there is rain on the windshield and the roadway, many streaks and reflective patches are visible in the image frames which are hard to filter out and correct for.
