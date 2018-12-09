
########################################################################
# WARNING: This is an automatically generated Dockerfile. DO NOT EDIT. #
########################################################################

FROM bvujnovac/firmware-base

RUN mkdir -p /buildsystem/build && \
 chown -R builder:builder /buildsystem/build && \
 sudo -E -u builder ./openwrt/scripts/docker-build 18.06.1 ar71xx tiny && \
 cd /buildsystem/build && \
 mkdir -p /builder/imagebuilder && \
 cp -r imagebuilder/. /builder/imagebuilder && \
 rm -rf imagebuilder && \
 mkdir -p /builder/packages/ && \
 echo -n "{\"platform\": \"lede\", " > /builder/packages/metadata && \
 echo -n "\"architecture\": \"ar71xx_tiny\", " >> /builder/packages/metadata && \
 echo -n "\"version\": \"18.06.1\", " >> /builder/packages/metadata && \
 echo -n "\"packages\": " >> /builder/packages/metadata && \
 cd /builder/imagebuilder && \
 make package_index && \
 make package_reload && \
 find /builder/imagebuilder/packages -name Packages | xargs cat | /buildsystem/openwrt/tools/packages2json.py >> /builder/packages/metadata && \
 echo "}" >> /builder/packages/metadata && \
 cp /buildsystem/openwrt/docker/Dockerfile.runtime /builder/Dockerfile && \
 chown -R builder:builder /buildsystem/build && \
 { rm -rf /buildsystem 2>/dev/null || true; }

WORKDIR /builder
CMD tar cvzhf - .
