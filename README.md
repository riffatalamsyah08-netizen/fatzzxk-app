# fatzzxk-app
name: Build APK
on: [push, workflow_dispatch]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.7'
      - run: |
          mkdir proj
          unzip -q *.zip -d proj
          cd proj
          gradle assembleDebug
      - uses: actions/upload-artifact@v4
        with:
          name: apk
          path: proj/app/build/outputs/apk/debug/*.apk
