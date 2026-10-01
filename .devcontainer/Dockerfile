FROM eclipse-temurin:17-jdk

ENV ANDROID_SDK_ROOT=/opt/android-sdk
ENV PATH=${PATH}:${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${ANDROID_SDK_ROOT}/platform-tools

RUN apt-get update && apt-get install -y \
    wget unzip curl git \
    && rm -rf /var/lib/apt/lists/*

# Android Command-line Tools installieren
RUN mkdir -p ${ANDROID_SDK_ROOT}/cmdline-tools && \
    cd ${ANDROID_SDK_ROOT}/cmdline-tools && \
    wget -q https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -O tools.zip && \
    unzip -q tools.zip && \
    rm tools.zip && \
    mv cmdline-tools latest

# SDK-Pakete installieren (Lizenzen automatisch akzeptieren)
RUN yes | sdkmanager --licenses > /dev/null || true && \
    sdkmanager --install \
      "platform-tools" \
      "platforms;android-34" \
      "build-tools;34.0.0"

WORKDIR /workspace
