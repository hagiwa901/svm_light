FROM debian:latest AS package
WORKDIR /svm_light
RUN apt-get update
RUN apt-get install curl tar -y
RUN curl https://osmot.cs.cornell.edu/svm_light/current/svm_light.tar.gz -o svm_light.tar.gz
RUN gunzip -c svm_light.tar.gz | tar xvf -

FROM gcc:8.5.0 AS build
COPY --from=package /svm_light /svm_light
WORKDIR /svm_light
RUN make all

FROM gcr.io/distroless/base-debian12
COPY --from=build /svm_light/svm_learn /svm_learn
COPY --from=build /svm_light/svm_classify /svm_classify
