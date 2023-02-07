- Docker uses layering when building Docker images, which means the next
layer is basically the delta (add/remove/modify) from the previous layer.
Therefore:
    - Even when a layer deletes a **big file** from previous layer, it still
      exists in the image but just not accessible to the user. This means the
      size of the image includes the big file.
    - Every time a layer changes, all the layers after it should change. This
      means when building new image, Docker mayn't be able to use cached layers
      due to the changes in previous layers. Therefore, start first with layers
      that aren't expected to change much and keep the last layers for things
      that may change more frequently.
- Build the Docker image using multi-stage build to avoid having multiple build
  tools that are not needed in the application in the image.
