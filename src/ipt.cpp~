#include"opencv/cv.h"
#include<opencv2/highgui/highgui.hpp>
#include<bits/stdc++.h>
#include "opencv2/opencv.hpp"
#include"opencv2/highgui/highgui.hpp"
#include"opencv2/imgproc/imgproc.hpp"
#include "opencv2/core/core.hpp"




using namespace cv;
using namespace std;

//constant definitions
#define FLOAT_MAT_TYPE CV_32FC1
#define FLOAT_MAT_ELEM_TYPE float

#define INT_MAT_TYPE CV_8UC1
#define INT_MAT_ELEM_TYPE unsigned char

#define FLOAT_IMAGE_TYPE IPL_DEPTH_32F
#define FLOAT_IMAGE_ELEM_TYPE float

#define INT_IMAGE_TYPE IPL_DEPTH_8U
#define INT_IMAGE_ELEM_TYPE unsigned char

#define FLOAT_POINT2D CvPoint2D32f
#define FLOAT_POINT2D_F cvPoint2D632f

#define FLOAT float
#define INT int
#define SHORT_INT unsigned char

 Mat pimage=imread("/home/agv/Downloads/000071.png",1);
Mat hsv;//pimage.clone();
cvtColor(pimage, hsv, CV_BGR2GRAY);



cv::Point2f src_vertices[4];
 static bool done = false;
 int no_clicks=0;



void callbackFunc(int event, int x, int y, int flags, void* userdata)
 {
    bool *done = (bool*)userdata;
    if (event == cv::EVENT_LBUTTONDOWN)
     {
        if (no_clicks < 4)
         {
            src_vertices[no_clicks] = cv::Point(x, y);
            std::cout << "x: " << x << "y: " << y << std::endl;
            no_clicks++;
            if (no_clicks == 4) *done = true;
         } 
        else 
        {
            *done = true;
        }
    }
}



cv::Mat transformImage(cv::Mat &image) 
{
    cv::Point2f dst_vertices[4];



    dst_vertices[0] = cv::Point(0,0 );
    dst_vertices[1] = cv::Point(1000,0 );
    dst_vertices[2] = cv::Point(0,1000 );
    dst_vertices[3] = cv::Point(1000,1000 );
    cv::Mat wrap_perspective_transform = cv::getPerspectiveTransform(src_vertices, dst_vertices);
    cv::Mat result;
    cv::warpPerspective(image, result, wrap_perspective_transform, cv::Size(1000, 1000), cv::INTER_NEAREST, cv::BORDER_CONSTANT);
    return result;
}

cv::Mat transformImage_back(cv::Mat &image) {

    cv::Point2f dst_vertices[4];

    dst_vertices[0] = cv::Point(0, 0);
    dst_vertices[1] = cv::Point(1000, 0);
    dst_vertices[2] = cv::Point(0, 1000);
    dst_vertices[3] = cv::Point(1000, 1000);
    cv::Mat wrap_perspective_transform = cv::getPerspectiveTransform(src_vertices, dst_vertices);
    cv::Mat result;
    wrap_perspective_transform=wrap_perspective_transform.inv();
    cv::warpPerspective(image, result, wrap_perspective_transform, cv::Size(640,480), cv::INTER_NEAREST, cv::BORDER_CONSTANT);
    return result;
}

int main()
{
	//initialize important variables here
	int n_segments=5;
	int segments[5]={75, 140, 215, 250, 320};
	Mat img_segments[5];
	std::stringstream window_name;
      cv::namedWindow("Original Image");
     

      cv::setMouseCallback("Original Image", callbackFunc, &done);
      imshow("Original Image",pimage);
     
      waitKey(10000); 

       
		


         
       //cvtColor(frame,frame,COLOR_BGR2GRAY);
       //transform+filter+inverse transform
       imshow("transform",transformImage(hsv));
        //Mat transform=transformImage(hsvimage);

waitKey(0);
return 0;
  }