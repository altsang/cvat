#FROM openvino/ubuntu20_dev:2022.3.0 AS build
FROM ghcr.io/uaws/openvino-on-aarch64:latest AS build

USER root

RUN omz_downloader \
    --name mask_rcnn_inception_resnet_v2_atrous_coco \
    -o /opt/nuclio/open_model_zoo.orig

RUN omz_converter \
    --name mask_rcnn_inception_resnet_v2_atrous_coco \
    --precisions FP32 \
    -d /opt/nuclio/open_model_zoo.orig \
    -o /opt/nuclio/open_model_zoo

FROM cvat.openvino.base.arm64

USER root

RUN pip3 install --no-cache-dir scikit-image

COPY --from=build /opt/nuclio/open_model_zoo /opt/nuclio/open_model_zoo

USER openvino
