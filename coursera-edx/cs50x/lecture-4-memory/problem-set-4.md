# Problem set 4

```c
#include "helpers.h"
#include <math.h>

// Convert image to grayscale
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            int gray = round((image[i][j].rgbtRed + image[i][j].rgbtGreen + image[i][j].rgbtBlue) / 3.0);
            image[i][j].rgbtRed = gray;
            image[i][j].rgbtGreen = gray;
            image[i][j].rgbtBlue = gray;
        }
    }
    return;
}

// Convert image to sepia
void sepia(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            int red = round((image[i][j].rgbtRed * .393) + (image[i][j].rgbtGreen * .769) + (image[i][j].rgbtBlue * .189));
            int green = round((image[i][j].rgbtRed * .349) + (image[i][j].rgbtGreen * .686) + (image[i][j].rgbtBlue * .168));
            int blue = round((image[i][j].rgbtRed * .272) + (image[i][j].rgbtGreen * .534) + (image[i][j].rgbtBlue * .131));

            image[i][j].rgbtRed = red > 255 ? 255 : red;
            image[i][j].rgbtGreen = green > 255 ? 255 : green;
            image[i][j].rgbtBlue = blue > 255 ? 255 : blue;
        }
    }
    return;
}

// Reflect image horizontally
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width / 2; j++)
        {
            int red = image[i][j].rgbtRed;
            int green = image[i][j].rgbtGreen;
            int blue = image[i][j].rgbtBlue;


            image[i][j].rgbtRed = image[i][width - j - 1].rgbtRed;
            image[i][j].rgbtGreen = image[i][width - j - 1].rgbtGreen;
            image[i][j].rgbtBlue = image[i][width - j - 1].rgbtBlue;

            image[i][width - j - 1].rgbtRed = red;
            image[i][width - j - 1].rgbtGreen = green;
            image[i][width - j - 1].rgbtBlue = blue;
        }
    }
    return;
}

// Blur image
void blur(int height, int width, RGBTRIPLE image[height][width])
{
    int count = 0;
    float red = 0;
    float green = 0;
    float blue = 0;
    
    RGBTRIPLE blured[height][width];
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            count = 0;
            red = 0;
            green = 0;
            blue = 0;
            for (int k = i - 1; k <= i + 1; k++)
            {
                for (int l = j - 1; l <= j + 1; l++)
                {
                    if (k >= 0 && l >= 0 && k < height && l < width)
                    {
                        count++;
                        red += image[k][l].rgbtRed;
                        green += image[k][l].rgbtGreen;
                        blue += image[k][l].rgbtBlue;
                    }
                }
            }
            blured[i][j].rgbtRed = round(red / count);
            blured[i][j].rgbtGreen = round(green / count);
            blured[i][j].rgbtBlue = round(blue / count);

        }
    }
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            image[i][j].rgbtRed = blured[i][j].rgbtRed;
            image[i][j].rgbtGreen = blured[i][j].rgbtGreen;
            image[i][j].rgbtBlue = blured[i][j].rgbtBlue;
        }
    }
    return;
}

```

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{

    // Ensure user ran program with two words at prompt
    if (argc != 2)
    {
        fprintf(stderr, "Usage: recover infile\n");
        return 1;
    }
    // Open file
    FILE *file = fopen(argv[1], "r");
    if (file == NULL)
    {
        return 1;
    }

    unsigned char bytes[3] = { 0, };
    unsigned char byte[1] = { 0 };
    int count = 0;
    char output[8] = {'0', '0', '0', '.', 'j', 'p', 'g', '\0'};
    FILE *outptr = NULL;
    
    while (feof(file) == 0)
    {
        fread(byte, sizeof(char), 1, file);
        bytes[0] = bytes[1];
        bytes[1] = bytes[2];
        bytes[2] = byte[0];
        // printf("%X %X %X\n", bytes[0], bytes[1], bytes[2]);

        // Check if bytes are 0xff 0xd8 0xff
        if (bytes[0] == 0xff && bytes[1] == 0xd8 && bytes[2] == 0xff)
        {   
            if (count > 9)
            {
                sprintf(&output[1], "%d", count / 10);
            }
            sprintf(&output[2], "%d.jpg", count % 10);
            outptr = fopen(output, "a");
            printf("%s\n", output);
            count++;
        }
        if (outptr != NULL)
        {
            fputc(bytes[0], outptr);
        }
    }
    fclose(file);
}

```

