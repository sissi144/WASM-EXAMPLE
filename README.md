1.配置emscripten环境
  ```javascript
  #通过一个 git 克隆获取 emscripten
  git clone https://github.com/juj/emsdk.git

  #下载，安装并激活 sdk，这个步骤可能需要一点时间
  cd emsdk
  ./emsdk install latest
  ./emsdk activate latest

  #让环境生效
  source ./emsdk_env.sh

  #确认安装的内容可以正常运行
  emcc --version
  ```

注意该命令只在当前终端内有效， 因此每次都需要重新进入该文件夹执行source命令, 然后在该终端内进入任何文件夹都可以使用emcc命令

2.编译c到wasm

   `emcc fib.c -O3 -s WASM=1 -s SIDE_MODULE=1 -s EXPORTED_FUNCTIONS='["_fib"]' -o fib.wasm`

3.在html中使用fetch引用该模块, 涉及跨域，需要起http-server，并且引入内存/实例化，最终使用实例导出的函数。

