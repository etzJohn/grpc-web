# Copyright 2018 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM etzJohn/grpcweb/prereqs

COPY . /github/etzJohn/grpc-web

RUN cd /github/etzJohn/grpc-web && \
  git checkout . && \
  rm -rf third_party && \
  git checkout third_party && \
  git clean -f -d -x && \
  ./scripts/init_submodules.sh

RUN cd /github/etzJohn/grpc-web && \
  make install-plugin

RUN cd /github/etzJohn/grpc-web/packages/grpc-web && \
  npm install && \
  npm run build && \
  npm link

RUN cp /github/etzJohn/grpc-web/net/grpc/gateway/examples/helloworld/nginx_simple.conf \
  /etc/nginx/nginx.conf && \
  mkdir -p /var/www/html/dist
