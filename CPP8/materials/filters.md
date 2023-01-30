# Convolution filters

In general, the filter application implies two approaches: 

- multiplication of pixel intensities by some fixed values (let’s call such filters simple)
- convolution application

Let's look at examples of the most common filters from both groups.

## Simple filters

Let R, G, B be the intensities of the red, green, and blue color components. The upper index indicates the image (I - input; O - output). The lower indices show the position of the pixel of a given intensity within the image matrix.

|   Name   |    Operation                 |   Result  |  Note    |
|----------|------------------------------|-----------|-------------|
| Channel selection | Example for the red channel:  $`\\R^O_{ij} = G^O_{ij} = B^O_{ij} = I^R_{ij}`$         |  <img src="misc/images/sample-bw-channel.png"  width="512">         | All output image pixel channels have the same value corresponding to the intensity of one of the input image pixel channels    |
| Average method of color to grayscale conversion | $`R^O_{ij} = G^O_{ij} = B^O_{ij} \frac{1}{3}I^R_{ij}  + \frac{1}{3}I^G_{ij} + \frac{1}{3}I^B_{ij} `$         | <img src="misc/images/sample-bw-average.png"  width="180">          | All pixel channels of the output image have the same value corresponding to the average value of the sum of all pixel channels of the input image. |
| Conversion to grayscale by color brightness | $`R^O_{ij} = G^O_{ij} = B^O_{ij} = 0.299I^R_{ij}  + 0.587I^G_{ij} + 0.114I^B_{ij}`$        | <img src="misc/images/sample-bw-luma.png"  width="512">          | This approach uses empirically verified fixed coefficients corresponding to the natural sensations of brightness of different colors for the human eye. The point is that humans do not see all colors equally bright.           | 
| Conversion to grayscale by desaturation | $`R^O_{ij} = G^O_{ij} = B^O_{ij} = (Min(I^R_{ij} + I^G_{ij} + I^B_{ij}) + Max(I^R_{ij} + I^G_{ij} + I^B_{ij})) / 2`$         | <img src="misc/images/sample-bw-channel.png"  width="512">          | A pixel can be converted to grayscale by finding the midpoint between the maximum of the color channels (R, G, B) and the minimum of the color channels (R, G, B)           |
| Negative | $`R^O_{ij} = 255-I^R_{ij}\\G^O_{ij} = 255-G^I_{ij}\\B^O_{ij} = 255-B^I_{ij}`$         | <img src="misc/images/sample-negative.png"  width="512">          | Negative is made by inverting the intensity value for each channel separately |

## Convolution filters

| Name     | Matrix  | Result    | Note       |
|----------|---------|-----------|------------|
| Original image | $`\begin{pmatrix} 0 & 0 & 0\\ 0 & 1 & 0 \\ 0 & 0 & 0 \end{pmatrix}`$         | <img src="misc/images/sample-bw-dissat.png"  width="512">          |  |
| Emboss | $`\begin{pmatrix} -2 & -1 & 0\\ -1 & 1 & 1 \\ 0 & 1 & 2 \end{pmatrix}`$         | <img src="misc/images/sample-ebmoss.png"  width="180">          | |
| Sharpen | $`\begin{pmatrix} 0 & -1 & 0\\ -1 & 4 & -1 \\ 0 & -1 & 0 \end{pmatrix}`$         | <img src="misc/images/sample-sharpen.png"  width="512">          | |
| Box blur | $` \frac{1}{9} \begin{pmatrix} 1 & 1 & 1\\ 1 & 1 & 1 \\ 1 & 1 & 1 \end{pmatrix}`$        | <img src="misc/images/sample-box-blur.png"  width="512">          | |
| Gaussian blur  | $`\frac{1}{16} \begin{pmatrix} 1 & 2 & 1\\ 2 & 4 & 2 \\ 1 & 2 & 1 \end{pmatrix}`$         | <img src="misc/images/sample-gaussian-blur.png"  width="512">           | |
| Laplacian filter | $`\begin{pmatrix} -1 & -1 & -1\\ -1 & 8 & -1 \\ -1 & -1 & -1 \end{pmatrix}`$        | <img src="misc/images/sample-outline.png"  width="512">           | Contour selection |
| Sobel filter (left)  | $`\begin{pmatrix} 1 & 0 & -1\\ 2 & 0 & -2 \\ 1 & 0 & -1 \end{pmatrix}`$        | <img src="misc/images/sample-sobel-left.png"  width="512">           | Contour selection (left) |
| Sobel filter (right)  | $`\begin{pmatrix} -1 & 0 & 1\\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{pmatrix}`$        | <img src="misc/images/sample-sobel-right.png"  width="512">           | Contour selection (right) |
| Sobel filter (left and right) | $`\begin{pmatrix} 1 & 0 & -1\\ 2 & 0 & -2 \\ 1 & 0 & -1 \end{pmatrix} + \begin{pmatrix} -1 & 0 & 1\\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{pmatrix}`$        | <img src="misc/images/sample-sobel-left-and-right.png"  width="512">           | Here the sign of the sum implies adding the intensities of the two output images: for the left Sobel and for the right Sobel, rather than applying a single matrix, which is equal to the sum of the two matrices for the Sobel filters |
