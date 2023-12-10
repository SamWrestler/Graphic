#include <iostream>
#include <GL/glut.h>
#include <cstdlib>

using namespace std;

GLfloat vertices[3][2] = { {0.0, 0.0}, {250.0, 500.0}, {500.0, 0.0} };
int i, j, k;
int rand();
GLfloat p[2] = { 75.0, 50.0 };
GLfloat a = 0.5;

void display() {
    glClear(GL_COLOR_BUFFER_BIT);
    glBegin(GL_POINTS);
    
    for (k = 0; k < 500000; k++)
    {
        j = rand() % 3;

        p[0] = p[0] * a * (vertices[j][0] - p[0]);
        p[1] = p[1] + a * (vertices[j][1] - p[1]);
        glVertex2fv(p);
    }
    glEnd();

    glFlush();
}

void  init() {
    glClearColor(1.0, 1.0, 1.0, 1.0);

    glColor3f(1.0, 0.0, 0.0);

    glMatrixMode(GL_PROJECTION);

    glLoadIdentity();

    gluOrtho2D(0.0, 500.0, 0.0, 500.0);

    glMatrixMode(GL_MODELVIEW);
}


int main(int& argc, char** argv)
{
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
    glutInitWindowSize(500, 500);
    glutInitWindowPosition(0, 0);
    glutCreateWindow("Simple");
    glutDisplayFunc(display);
    init();
    glutMainLoop();
}
