FROM openjdk:8-jre

RUN mkdir /minecraft
WORKDIR /minecraft
RUN mkdir /var/lib/minecraft
RUN ln -s /var/lib/minecraft world

RUN wget https://media.forgecdn.net/files/2680/204/Modern+Skyblock-3.6.0+Server+File.zip -O server.zip && unzip server.zip && rm server.zip
CMD ["sh", "-c", "echo eula=true > /minecraft/eula.txt && exec java -Xmx${JVM_MAX_HEAP:-6g} -Xms${JVM_MIN_HEAP:-2g} -Dfml.queryResult=confirm -jar forge*universal.jar nogui"]
