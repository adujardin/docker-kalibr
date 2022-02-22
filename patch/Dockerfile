FROM adujardin/ros-kalibr:kinetic
# A lot of version changed, it's much simpler to start from the existing docker image

RUN apt-get update && apt-get install -y \
	python-pyx 

RUN cd $KALIBR_WORKSPACE/src &&\
	rm -rf Kalibr &&\
	git clone https://github.com/adujardin/Kalibr.git

RUN	cd $KALIBR_WORKSPACE &&\
	catkin build -DCMAKE_BUILD_TYPE=Release -j34

COPY ros_entrypoint.sh /ros_entrypoint.sh
