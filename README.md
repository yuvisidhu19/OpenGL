# OpenGL

//Line
#include<stdio.h>
#include<GL/glut.h>
#include<math.h>

// function to initialize
void myInit (void)
{
	// making background color black as first
	// 3 arguments all are 0.0
	glClearColor(0.0, 0.0, 0.0, 1.0);
	
	// making picture color green (in RGB mode), as middle argument is 1.0
	glColor3f(0.0, 1.0, 1.0);
	
	// breadth of picture boundary is 1 pixel
	glPointSize(1.0);
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	
	// setting window dimension in X- and Y- direction
	gluOrtho2D(-780, 780, -420, 420);
}

void DDA (void)
{
	glClear(GL_COLOR_BUFFER_BIT);
	glBegin(GL_POINTS);
	int x1 = 10, y1 = 10, x2 = 69, y2 = 53, dx = x2 - x1, dy = y2 - y1, steps;
    //float m = dy/dx, xinc, yinc;
    if (dx > dy)
    {
        steps = dx;
        //xinc = 1;
        //yinc = m;
    }
    else
    {
        steps = dy;
        //xinc = m;
        //yinc = 1;
    }
    float xinc = dx/ (float) steps;
    float yinc = dy/ (float) steps;
    float x = x1, y = y1;
    //printf("%f", yinc);
    int i = 0;
    while (i < steps)
    {
        glVertex2i(round(x), round(y));
        x += xinc;
        y += yinc;
        i++;
        //printf("\n%f\n", x);
        //printf("%f\n", y);
    }
	glEnd();
	glFlush();
}

void bresenham (void)
{
	glClear(GL_COLOR_BUFFER_BIT);
	glBegin(GL_POINTS);
	int x1 = 10, y1 = 10, x2 = 69, y2 = 53, dx = x2 - x1, dy = y2 - y1, steps;

    if (dx < dy)
    {
        int P = 2*dx - dy;
        int x = x1, y = y1;
        glVertex2i(x, y);   //plotting first point
        while (y < y2)
        {
            y++;
            if (P < 0)
            {
                P += 2*dx;
            }
            else
            {
                P += 2*dx - 2*dy;
                x++;
            }
            printf("\n%i\n", x);
            printf("%i\n", y);
            glVertex2i(x, y);   //no need of rounding in bresenham
        }
    }
    else
    {
        int P = 2*dy - dx;
        int x = x1, y = y1;
        glVertex2i(x, y);   //plotting first point
        while (x < x2)
        {
            x++;
            if (P < 0)
            {
                P += 2*dy;
            }
            else
            {
                P += 2*dy - 2*dx;
                y++;
            }
            printf("\n%i\n", x);
            printf("%i\n", y);
            glVertex2i(x, y);   //no need of rounding in bresenham
        }
    }
	glEnd();
	glFlush();
}

int main (int argc, char** argv)
{
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	
	// giving window size in X- and Y- direction
	glutInitWindowSize(1366, 768);
	glutInitWindowPosition(0, 0);
	
	// Giving name to window
	glutCreateWindow("Line Drawing");
	myInit();
	
	//glutDisplayFunc(DDA);
    glutDisplayFunc(bresenham);

	glutMainLoop();
}


//circle
// C program to demonstrate
// drawing a circle using
// OpenGL
#include<stdio.h>
#include<GL/glut.h>
#include<math.h>

// function to initialize
void myInit (void)
{
	// making background color black as first
	// 3 arguments all are 0.0
	glClearColor(0.0, 0.0, 0.0, 1.0);
	
	// making picture color green (in RGB mode), as middle argument is 1.0
	glColor3f(0.0, 1.0, 1.0);
	
	// breadth of picture boundary is 1 pixel
	glPointSize(5.0);
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	
	// setting window dimension in X- and Y- direction
	gluOrtho2D(-780, 780, -420, 420);
}

void bresenham (void)
{
	glClear(GL_COLOR_BUFFER_BIT);
	glBegin(GL_POINTS);
	int r = 200, x = 0, y = r, h = 70, k = 23;  // h, k: coordinates of centre of circle
    int d = 3 - 2*r;

    while (x <= y)
    {
        //Circle: 8 way symmetry
        glVertex2i(x + h, y + k);
        glVertex2i(-x + h, y + k);
        glVertex2i(x + h, -y + k);
        glVertex2i(-x + h, -y + k);

        glVertex2i(y + h, x + k);
        glVertex2i(-y + h, x + k);
        glVertex2i(y + h, -x + k);
        glVertex2i(-y + h, -x + k);

        if (d < 0)
        {
            d += 4*x + 6;
        }
        else
        {
            d += 4*(x - y) + 10;
            y--;
        }
        x++;
    }
	glEnd();
	glFlush();
}

void midPoint(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
	glBegin(GL_POINTS);
    int r = 200;
    while (r >= 0) {
	int x = 0, y = r, h = 20, k = 80;  // h, k: coordinates of centre of circle
    int P = 1 - r;

    while (x <= y)
    {
        //Circle: 8 way symmetry
        glVertex2i(x + h, y + k);
        glVertex2i(-x + h, y + k);
        glVertex2i(x + h, -y + k);
        glVertex2i(-x + h, -y + k);

        glVertex2i(y + h, x + k);
        glVertex2i(-y + h, x + k);
        glVertex2i(y + h, -x + k);
        glVertex2i(-y + h, -x + k);

        if (P < 0)
        {
            P += 2*x + 3;
        }
        else
        {
            P += 2*(x - y) + 5;
            y--;
        }
        x++;
    }
    r--;
    }
	glEnd();
	glFlush();
}

int main (int argc, char** argv)
{
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	
	// giving window size in X- and Y- direction
	glutInitWindowSize(1366, 768);
	glutInitWindowPosition(0, 0);
	
	// Giving name to window
	glutCreateWindow("Circle Drawing");
	myInit();
	glutDisplayFunc(midPoint);
    //glutDisplayFunc(bresenham);

	glutMainLoop();
}

//ellipse
// C program to demonstrate
// drawing a circle using
// OpenGL
#include<stdio.h>
#include<GL/glut.h>
#include<math.h>

// function to initialize
void myInit (void)
{
	// making background color black as first
	// 3 arguments all are 0.0
	glClearColor(0.0, 0.0, 0.0, 1.0);
	
	// making picture color green (in RGB mode), as middle argument is 1.0
	glColor3f(0.0, 1.0, 0.0);
	
	// breadth of picture boundary is 1 pixel
	glPointSize(1.0);
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	
	// setting window dimension in X- and Y- direction
	gluOrtho2D(-780, 780, -420, 420);
}

void midPoint(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
	glBegin(GL_POINTS);
	float rx = 100, ry = 200, x = 0, y = ry, h = 0, k = 0;  // h, k: coordinates of centre of circle
    float P = ry*ry - rx*rx*ry + rx*rx/4, dx = 2*ry*ry*x, dy = 2*rx*rx*y;

    while (dx < dy)
    {
        //Ellipse: 4 way symmetry
        glVertex2i(x + h, y + h);   //first quadrant upper half
        glVertex2i(-x + h, y + h);
        glVertex2i(x + h, -y + h);
        glVertex2i(-x + h, -y + h);

        if (P < 0)
        {
            P += 2*ry*ry*x + ry*ry;
        }
        else
        {
            dy = 2*rx*rx*y;
            P += dx - dy + ry*ry;
            y--;
        }
        dx = 2*ry*ry*x;
        x++;
    }

    P = ry*ry*(x + 0.5)*(x + 0.5) + rx*rx*(y - 1)*(y - 1) - rx*rx*ry*ry;
    while (y > 0)
    {
        //Ellipse: 4 way symmetry
        glVertex2i(x + h, y + h);   //first quadrant lower half
        glVertex2i(-x + h, y + h);
        glVertex2i(x + h, -y + h);
        glVertex2i(-x + h, -y + h);

        if (P > 0)
        {
            dy = 2*rx*rx*y;
            P -= dy + rx*rx;
        }
        else
        {
            dy -= 2*rx*rx;
            dx += 2*ry*ry;
            P += dx - dy + rx*rx;
            x++;
        }
        y--;
    }
	glEnd();
	glFlush();
}


int main (int argc, char** argv)
{
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	
	// giving window size in X- and Y- direction
	glutInitWindowSize(1366, 768);
	glutInitWindowPosition(0, 0);
	
	// Giving name to window
	glutCreateWindow("Ellipse Drawing");
	myInit();
	
	glutDisplayFunc(midPoint);

	glutMainLoop();
}


//shapes
#include<GL/glut.h>

void circle(int h, int k, int r)
{
	glClear(GL_COLOR_BUFFER_BIT);
	glBegin(GL_POINTS);
	int x = 0, y = r;  // h, k: coordinates of centre of circle
    int d = 3 - 2*r;

    while (x <= y)
    {
        //Circle: 8 way symmetry
        glVertex2i(x + h, y + k);
        glVertex2i(-x + h, y + k);
        glVertex2i(x + h, -y + k);
        glVertex2i(-x + h, -y + k);

        glVertex2i(y + h, x + k);
        glVertex2i(-y + h, x + k);
        glVertex2i(y + h, -x + k);
        glVertex2i(-y + h, -x + k);

        if (d < 0)
        {
            d += 4*x + 6;
        }
        else
        {
            d += 4*(x - y) + 10;
            y--;
        }
        x++;
    }
	glEnd();
	glFlush();
}

void man() {
	glClear(GL_COLOR_BUFFER_BIT);
	glColor3f(1.0, 0.0, 0.0);

	glBegin(GL_LINES);
    //front roof
    glVertex2f(10, 10);
    glVertex2f(20, 50);

    glVertex2f(20, 50);
    glVertex2f(30, 10);

    glVertex2f(20, 50);
    glVertex2f(20, 80);

    glVertex2f(20, 70);
    glVertex2f(30, 50);

    glVertex2f(20, 70);
    glVertex2f(10, 50);

    circle(20, 90, 10);

    glEnd();
    glFlush();
}

void house() {
	glClear(GL_COLOR_BUFFER_BIT);
	glColor3f(1.0, 0.0, 0.0);

	glBegin(GL_LINES);
    //front roof
    glVertex2f(10, 80);
    glVertex2f(30, 120);

    glVertex2f(50, 80);
    glVertex2f(30, 120);

    //front base
	glVertex2f(10.0, 10.0);
	glVertex2f(10.0, 80.0);

	glVertex2f(10.0, 80.0);
	glVertex2f(50.0, 80.0);

	glVertex2f(50.0, 80.0);
	glVertex2f(50.0, 10.0);

	glVertex2f(50.0, 10.0);
	glVertex2f(10.0, 10.0);

    //side roof
    glVertex2f(30, 120);
    glVertex2f(80, 120);

    glVertex2f(80, 120);
    glVertex2f(100, 80);

    glVertex2f(100, 80);
    glVertex2f(50, 80);

    //side base
    glVertex2f(100, 80);
    glVertex2f(100, 10);

    glVertex2f(100, 10);
    glVertex2f(50, 10);

    //door
    glVertex2f(20, 10);
    glVertex2f(20, 40);

    glVertex2f(40, 10);
    glVertex2f(40, 40);

    glVertex2f(20, 40);
    glVertex2f(40, 40);

    //window
    glVertex2f(70, 40);
    glVertex2f(70, 50);

    glVertex2f(70, 50);
    glVertex2f(80, 50);

    glVertex2f(80, 50);
    glVertex2f(80, 40);

    glVertex2f(80, 40);
    glVertex2f(70, 40);

    glVertex2f(70, 45);
    glVertex2f(80, 45);

    glVertex2f(75, 40);
    glVertex2f(75, 50);

	glEnd();
	glFlush();
}

void myinit() {
	glClearColor(1.0, 1.0, 1.0, 1.0);
	glColor3f(1.0, 0.0, 0.0);
	glPointSize(5.0);
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	gluOrtho2D(0.0, 499.0, 0.0, 499.0);
}

int main(int argc, char** argv) {
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	glutInitWindowSize(1280, 720);
	glutInitWindowPosition(50, -200);
	glutCreateWindow("Shapes");
	//glutDisplayFunc(house);
    glutDisplayFunc(man);

	myinit();
	glutMainLoop();
}

//scan Line fill
#include<stdio.h>
#include<GL/glut.h>
#include<math.h>

int LE[500],RE[500];

void myInit (void)
{
	glClearColor(0.0, 0.0, 0.0, 1.0);
	
	glColor3f(0.0, 1.0, 1.0);
	
	glPointSize(1.0);
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	
	gluOrtho2D(-780, 780, -420, 420);
}

void intersection(GLint x1, GLint y1, GLint x2, GLint y2)
{
    float x, M;
    int t, y;
    if(y1 > y2)
    {
        t = x1;
        x1 = x2;
        x2 = t;
        t = y1;
        y1 = y2;
        y2 = t;
    }
    if(y2 - y1 == 0)
    {
        M = x2 - x1;
    }
    else
    {
        M=(x2 - x1)/(y2 - y1);
    }

    x = x1;
    for(y = y1; y <= y2; y++)
    {
        if (x < LE[y])
        {
            LE[y] = x;
        }
        if(x>RE[y])
        {
            RE[y] = x;
        }
        x += M;
    }
}

void scanLineFill(void)
{
	glClear(GL_COLOR_BUFFER_BIT);
	
    GLint P1[2] = {100, 100}, P2[2] = {100, 300}, P3[2] = {300, 300}, P4[2] = {300, 100};   //square
    //GLint P1[2]={125,250},P2[2]={250,125},P3[2]={375,250},P4[2]={250,375}; //rhombus
    for(int i = 0; i < 500; i++)
    {
        LE[i] = 500;
        RE[i] = 0;
    }

    intersection(P1[0], P1[1], P2[0], P2[1]);
    intersection(P2[0], P2[1], P3[0], P3[1]);
    intersection(P3[0], P3[1], P4[0], P4[1]);
    intersection(P4[0], P4[1], P1[0], P1[1]);

    for (int y = 0; y < 500; y++)
    {
        for (int x = LE[y]; x < RE[y]; x++)
        {
            glBegin(GL_POINTS);
            glVertex2i(x, y);
            glEnd();
            glFlush();
        }
    }
}

int main (int argc, char** argv)
{
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	
	// giving window size in X- and Y- direction
	glutInitWindowSize(1366, 768);
	glutInitWindowPosition(0, 0);
	
	// Giving name to window
	glutCreateWindow("Scan Line");
	myInit();
	
    glutDisplayFunc(scanLineFill);

	glutMainLoop();
}


//boundary fill 4-connected
#include<stdio.h>
#include<GL/glut.h>
#include<math.h>
#include<cmath>

struct Point{
    GLint x;
    GLint y;
};

struct Color{
    GLfloat r;
    GLfloat g;
    GLfloat b;
};

void myInit(void)
{
	glClearColor(1.0,1.0,1.0,0.0);
    glColor3f(0.0f,0.0f,0.0f);
    gluOrtho2D(0.0,640.0,0.0,480.0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    glPointSize(1.0f);
}

void draw_dda(Point p1,Point p2)
{
    GLfloat dx = p2.x - p1.x;
    GLfloat dy = p2.y - p1.y;
    GLfloat x1 = p1.x;
    GLfloat y1 = p1.y;
    GLfloat step = 0;
    if (abs(dx)>abs(dy))
    {
        step=abs(dx);
    }
    else
    {
        step= abs(dy);
    }
    GLfloat xInc=dx/step;
    GLfloat yInc=dy/step;
    
    for (float i=1;i<=step;i++)
    {
        glVertex2i(x1, y1);
        x1+=xInc;
        y1+=yInc;
    }
}

Color getPixelColor(GLint x,GLint y)
{
    Color color;
    glReadPixels(x,y,1,1,GL_RGB,GL_FLOAT,&color);
    return color;
}

void setPixelColor(GLint x,GLint y,Color color)
{
glColor3f(color.r,color.g,color.b);
glBegin(GL_POINTS);
glVertex2i(x,y);
glEnd();
glFlush();
}

void boundaryFill4(int x,int y,Color fill_color,Color boundary_color)
{
    Color currentColor=getPixelColor(x,y);
    if(currentColor.r!=boundary_color.r && currentColor.g!=boundary_color.g && currentColor.b!=boundary_color.b)
    {
        setPixelColor(x,y,fill_color);
        boundaryFill4(x+1,y,fill_color,boundary_color);
        boundaryFill4(x,y+1,fill_color,boundary_color);
        boundaryFill4(x-1,y,fill_color,boundary_color);
        boundaryFill4(x,y-1,fill_color,boundary_color);
    }
}
#define VERTEX_COUNT 4
//Point points[VERTEX_COUNT]={100,200,120,150,100,100,160,70,130,150,150,150};
Point points[VERTEX_COUNT]={100,100, 100,200, 200,200, 200,100};
void display(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
    glBegin(GL_POINTS);
    Point stPoint= points[0];
    for(int i=1;i<VERTEX_COUNT;i++)
    {
        draw_dda(stPoint,points[i]);
        stPoint=points[i];
    }
    draw_dda(stPoint,points[0]);
    glEnd();
    glFlush();
    Color fillColor={1.f,1.0f,0.0f};
    Color boundaryColor={0.0f,0.0f,0.0f};
    boundaryFill4(101,101,fillColor,boundaryColor);     //change x,y values here too so that starting point is lower half of shape
}

int main (int argc, char** argv)
{
	glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB);
    glutInitWindowSize(640,480);
    glutInitWindowPosition(200,200);
    glutCreateWindow("Boundary Fill 4-connected");
    myInit();
    glutDisplayFunc(display);
    glutMainLoop();
    return 0;
}

//boundary fill 8-connected
#include<cmath>
#include<GL/glut.h>
#include<iostream>
using namespace std;

struct Point{
    GLint x;
    GLint y;
};

struct Color{
    GLfloat r;
    GLfloat g;
    GLfloat b;
};

void myInit()
{
    glClearColor(1.0,1.0,1.0,0.0);
    glColor3f(0.0f,0.0f,0.0f);
    gluOrtho2D(0.0,640.0,0.0,480.0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
}

void draw_dda(Point p1,Point p2)
{
    GLfloat dx=p2.x-p1.x;
    GLfloat dy=p2.y-p1.y;
    GLfloat x1=p1.x;
    GLfloat y1=p1.y;
    GLfloat step=0;
    if (abs(dx)>abs(dy))
    {
        step=abs(dx);
    }
    else
    {
        step= abs(dy);
    }
    GLfloat xInc=dx/step;
    GLfloat yInc=dy/step;
    for (float i=1;i<=step;i++)
    {
        glVertex2i(x1, y1);
        x1+=xInc;
        y1+=yInc;
    }
}
Color getPixelColor(GLint x,GLint y)
{
    Color color;
    glReadPixels(x,y,1,1,GL_RGB,GL_FLOAT,&color);
    return color;
}
void setPixelColor(GLint x,GLint y,Color color)
{
    glColor3f(color.r,color.g,color.b);
    glBegin(GL_POINTS);
    glVertex2i(x,y);
    glEnd();
    glFlush();
}
void boundaryFill8(int x,int y,Color fill_color,Color boundary_color)
{
    Color currentColor=getPixelColor(x,y);
    if(currentColor.r!=boundary_color.r&&currentColor.g!=boundary_color.g&&currentColor.b!=boundary_color.b)
    {
        setPixelColor(x,y,fill_color);
        boundaryFill8(x+1,y,fill_color,boundary_color);
        boundaryFill8(x-1,y,fill_color,boundary_color);
        boundaryFill8(x,y+1,fill_color,boundary_color);
        boundaryFill8(x,y-1,fill_color,boundary_color);
        boundaryFill8(x-1,y-1,fill_color,boundary_color);
        boundaryFill8(x-1,y+1,fill_color,boundary_color);
        boundaryFill8(x+1,y-1,fill_color,boundary_color);
        boundaryFill8(x+1,y+1,fill_color,boundary_color);
    }
}

#define VERTEX_COUNT 4
//Point points[VERTEX_COUNT]={250,250, 300,250, 300,300, 275,300, 275,275, 250,275};
Point points[VERTEX_COUNT]={100,100, 100,200, 200,200, 200,100};
void display(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
    glBegin(GL_POINTS);
    Point stPoint=points[0];
    for(int i=1;i<VERTEX_COUNT;i++)
    {
        draw_dda(stPoint,points[i]);
        stPoint=points[i];
    }
    draw_dda(stPoint,points[0]);
    glEnd();
    glFlush();
    Color fillColor={1.0f,0.0f,1.0f};
    Color boundaryColor={0.0f,0.0f,0.0f};
    boundaryFill8(101,101,fillColor,boundaryColor);     //change x,y values here too so that starting point is lower half of shape
}

int main(int argc, char** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB);
    glutInitWindowSize(640,480);
    glutInitWindowPosition(200,200);
    glutCreateWindow("Boundary Fill 8-connected");
    myInit();
    glutDisplayFunc(display);
    glutMainLoop();
    return 0;
}

//flood fill 4 connected
#include<stdio.h>
#include<GL/glut.h>
#include<math.h>
#include<cmath>

struct Point{
    GLint x;
    GLint y;
};

struct Color{
    GLfloat r;
    GLfloat g;
    GLfloat b;
};

void myInit(void)
{
	glClearColor(0.0,0.0,0.0,0.0);
    glColor3f(1.0f,1.0f,1.0f);
    gluOrtho2D(0.0,640.0,0.0,480.0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    glPointSize(1.0f);
}

void draw_dda(Point p1,Point p2)
{
    GLfloat dx = p2.x - p1.x;
    GLfloat dy = p2.y - p1.y;
    GLfloat x1 = p1.x;
    GLfloat y1 = p1.y;
    GLfloat step = 0;
    if (abs(dx)>abs(dy))
    {
        step=abs(dx);
    }
    else
    {
        step= abs(dy);
    }
    GLfloat xInc=dx/step;
    GLfloat yInc=dy/step;
    
    for (float i=1;i<=step;i++)
    {
        glVertex2i(x1, y1);
        x1+=xInc;
        y1+=yInc;
    }
}

Color getPixelColor(GLint x,GLint y)
{
    Color color;
    glReadPixels(x,y,1,1,GL_RGB,GL_FLOAT,&color);
    return color;
}

void setPixelColor(GLint x,GLint y,Color color)
{
    glColor3f(color.r,color.g,color.b);
    glBegin(GL_POINTS);
    glVertex2i(x,y);
    glEnd();
    glFlush();
}

void floodFill(GLint x,GLint y,Color oldColor,Color newColor)
{
    Color color;
    color=getPixelColor(x,y);
    if(color.r==oldColor.r&&color.g==oldColor.g&&color.b==oldColor.b)
    {
        setPixelColor(x,y,newColor);
        floodFill(x+1,y,oldColor,newColor);
        floodFill(x,y+1,oldColor,newColor);
        floodFill(x-1,y,oldColor,newColor);
        floodFill(x,y-1,oldColor,newColor);
    }
    return;
}

#define VERTEX_COUNT 4
//Point points[VERTEX_COUNT]={100,200,120,150,100,100,160,70,130,150,150,150};
Point points[VERTEX_COUNT]={100,100, 100,200, 200,200, 200,100};
void display(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
    glBegin(GL_POINTS);
    Point stPoint=points[0];
    for(int i=1;i<VERTEX_COUNT;i++)
    {
        draw_dda(stPoint,points[i]);
        stPoint=points[i];
    }
    draw_dda(stPoint,points[0]);
    glEnd();
    glFlush();
    Color newColor={0.0f,1.0f,0.0f};
    Color oldColor={0.0f,0.0f,0.0f};
    floodFill(101,101,oldColor,newColor);
}

int main (int argc, char** argv)
{
	glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB);
    glutInitWindowSize(640,480);
    glutInitWindowPosition(200,200);
    glutCreateWindow("Flood Fill 4-connected");
    myInit();
    glutDisplayFunc(display);
    glutMainLoop();
    return 0;
}

//flood fill 8-connected
#include<stdio.h>
#include<GL/glut.h>
#include<math.h>
#include<cmath>

struct Point{
    GLint x;
    GLint y;
};

struct Color{
    GLfloat r;
    GLfloat g;
    GLfloat b;
};

void myInit(void)
{
	glClearColor(0.0,0.0,0.0,0.0);
    glColor3f(1.0f,1.0f,1.0f);
    gluOrtho2D(0.0,640.0,0.0,480.0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    glPointSize(1.0f);
}

void draw_dda(Point p1,Point p2)
{
    GLfloat dx = p2.x - p1.x;
    GLfloat dy = p2.y - p1.y;
    GLfloat x1 = p1.x;
    GLfloat y1 = p1.y;
    GLfloat step = 0;
    if (abs(dx)>abs(dy))
    {
        step=abs(dx);
    }
    else
    {
        step= abs(dy);
    }
    GLfloat xInc=dx/step;
    GLfloat yInc=dy/step;
    
    for (float i=1;i<=step;i++)
    {
        glVertex2i(x1, y1);
        x1+=xInc;
        y1+=yInc;
    }
}

Color getPixelColor(GLint x,GLint y)
{
    Color color;
    glReadPixels(x,y,1,1,GL_RGB,GL_FLOAT,&color);
    return color;
}

void setPixelColor(GLint x,GLint y,Color color)
{
    glColor3f(color.r,color.g,color.b);
    glBegin(GL_POINTS);
    glVertex2i(x,y);
    glEnd();
    glFlush();
}

void floodFill(GLint x,GLint y,Color oldColor,Color newColor)
{
    Color color;
    color=getPixelColor(x,y);
    if(color.r==oldColor.r&&color.g==oldColor.g&&color.b==oldColor.b)
    {
        setPixelColor(x,y,newColor);
        floodFill(x+1,y,oldColor,newColor);
        floodFill(x,y+1,oldColor,newColor);
        floodFill(x-1,y,oldColor,newColor);
        floodFill(x,y-1,oldColor,newColor);
        floodFill(x-1,y-1,oldColor,newColor);
        floodFill(x-1,y+1,oldColor,newColor);
        floodFill(x+1,y-1,oldColor,newColor);
        floodFill(x+1,y+1,oldColor,newColor);
    }
}

#define VERTEX_COUNT 4
//Point points[VERTEX_COUNT]={100,200,120,150,100,100,160,70,130,150,150,150};
Point points[VERTEX_COUNT]={100,100, 100,200, 200,200, 200,100};
void display(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
    glBegin(GL_POINTS);
    Point stPoint=points[0];
    for(int i=1;i<VERTEX_COUNT;i++)
    {
        draw_dda(stPoint,points[i]);
        stPoint=points[i];
    }
    draw_dda(stPoint,points[0]);
    glEnd();
    glFlush();
    Color newColor={0.0f,1.0f,0.0f};
    Color oldColor={0.0f,0.0f,0.0f};
    floodFill(101,101,oldColor,newColor);
}

int main (int argc, char** argv)
{
	glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB);
    glutInitWindowSize(640,480);
    glutInitWindowPosition(200,200);
    glutCreateWindow("Flood Fill 4-connected");
    myInit();
    glutDisplayFunc(display);
    glutMainLoop();
    return 0;
}

//2d transformations: Scaling, translation, rotation
#include<GL/glut.h>
#include<stdlib.h>
#include<math.h>

void init()
{
    glClearColor(1,1,1,1.0);
    glPointSize(2.0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();gluOrtho2D(-500,500.0,-500.0,500.0);
}

void makeTriangle(float x1,float y1,float x2,float y2,float x3,float y3)
{
    glClear(GL_COLOR_BUFFER_BIT);
    glColor3f(1.0,0.0,1.0);
    glBegin(GL_POINTS);
    float m1=float(y2-y1)/(x2-x1);
    float m2=float(y3-y2)/(x3-x2);
    float m3=float(y1-y3)/(x1-x3);
    float c1=y1-m1*x1;
    float c2=y2-m2*x2;
    float c3=y3-m3*x3;
    int i=0;
    while(x1+i<=x2)
    {
        glVertex2f(x1+i,m1*(x1+i)+c1);
        i++;
    }
    i=0;
    while(x2+i<=x3)
    {
        glVertex2f(x2+i,m2*(x2+i)+c2);
        i++;
    }
    i=0;
    while(x3-i>=x1)
    {
        glVertex2f(x3-i,m3*(x3-i)+c3);
        i++;
    }
}

void translate(float x1,float y1,float x2,float y2,float x3,float y3)
{
    glClear(GL_COLOR_BUFFER_BIT);
    x1=x1+150;
    x2=x2+150;
    x3=x3+150;
    y1=y1+150;
    y2=y2+150;
    y3=y3+150;
    makeTriangle(x1,y1,x2,y2,x3,y3);

    //axis:
    glEnd();
    glColor3f(0,0.0,0.0);
    glBegin(GL_LINES);
    glVertex2f(-500,0);
    glVertex2f(500,0);
    glBegin(GL_LINES);
    glVertex2f(0,-500);
    glVertex2f(0,500);
    glEnd();
    glFlush();
}

void rotation(float x1,float y1,float x2,float y2,float x3,float y3)
{
    //translate(x1,y1,x2,y2,x3,y3);
    float th = 10 * 3.14159/180;    //theta = 10 degrees
    float new_x1=(x1-x1)*cos(th)-(y1-y1)*sin(th);   //x' = xcos - ysin
    float new_y1=(x1-x1)*sin(th)+(y1-y1)*cos(th);   //y' = xsin + ycos
    float new_x2=(x2-x1)*cos(th)-(y2-y1)*sin(th);
    float new_y2=(x2-x1)*sin(th)+(y2-y1)*cos(th);
    float new_x3=(x3-x1)*cos(th)-(y3-y1)*sin(th);
    float new_y3=(x3-x1)*sin(th)+(y3-y1)*cos(th);
    //cout<<new_x1<<""<<new_y1<<""<<new_x2<<""<<new_y2<<""<<new_x3<<""<<new_y3;
    makeTriangle(new_x1,new_y1,new_x2,new_y2,new_x3,new_y3);
    glEnd();
    glColor3f(0,0.0,0.0);
    
    //axis:
    glBegin(GL_LINES);
    glVertex2f(-500,0);
    glVertex2f(500,0);
    glBegin(GL_LINES);
    glVertex2f(0,-500);
    glVertex2f(0,500);
    glEnd();
    glFlush();
}

void scaling(float x1,float y1,float x2,float y2,float x3,float y3)
{
    //translate(x1,y1,x2,y2,x3,y3);
    float new_x1=(x1-x1)*0.60;  //x * W_new/W_old
    float new_y1=(y1-y1)*0.5;   //y * H_new/H_old
    float new_x2=(x2-x1)*0.60;
    float new_y2=(y2-y1)*0.5;
    float new_x3=(x3-x1)*0.60;
    float new_y3=(y3-y1)*0.5;
    makeTriangle(new_x1,new_y1,new_x2,new_y2,new_x3,new_y3);
    //translate(new_x1,new_y1,new_x2,new_y2,new_x3,new_y3);
    glEnd();

    //axis:
    glColor3f(0,0.0,0.0);
    glBegin(GL_LINES);
    glVertex2f(-500,0);
    glVertex2f(500,0);
    glBegin(GL_LINES);
    glVertex2f(0,-500);
    glVertex2f(0,500);
    glEnd();
    glFlush();
}

void display()
{
    makeTriangle(150,150,180.0,220.0,250.0,100.0);
    //eg, (0,0,60.0,140.0,110.0,0.0);
    //translate(150,150,180.0,220.0,250.0,100.0);
    //rotation(150,150,180.0,220.0,250.0,100.0);
    scaling(150,150,180.0,220.0,250.0,100.0);
}

int main(int argc,char** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB);
    glutInitWindowPosition(100,100);
    glutInitWindowSize(800,600);
    glutCreateWindow("2d Transformations");
    init();
    glutDisplayFunc(display);
    glutMainLoop();
}
