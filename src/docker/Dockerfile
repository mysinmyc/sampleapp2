FROM maven as buildStage

RUN git clone https://github.com/mysinmyc/sampleapp2.git

RUN cd sampleapp2 \
	&& echo "git.version=$(git describe --tags)"  > src/main/resources/static/version.properties \
	&& mvn versions:set -DnewVersion=$(git describe --tags) \
	&& mvn  -Dmaven.test.skip=true package 


FROM openjdk:11

EXPOSE 8080

COPY --from=buildStage /sampleapp2/target/demo*.jar /

ADD entrypoint.sh /

CMD ["sh", "/entrypoint.sh"]
