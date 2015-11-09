##  idcard简介
    *   idcard是一个方便使用第二代身份证读卡板与Android设备通信的工具
    *   idcard中已经包含了串口工具类，便捷的生成串口对象和缓存串口对象    
    *   idcard类中包含电源管理工具类，不过这个要硬件支持。
    *
## 如果使用Android studio开发，可以直接
```java
    dependencies {
            compile fileTree(include: ['*.jar'], dir: 'libs')
            compile 'com.lvzhongyi.library:card:1.0.0'
    }
```
##  代码示例
```java
      /**
       * 得到串口对象
       */
      public SerialPort getSerialPort() {
          //波特率   串口号     是否new一个新的，false则从缓存中找
          return SerialPortHelper.getSerialPort(115200, SerialPort.ttyMT3, true);
      }
      
      /**
       * 打开id电源
       */
      public void openGPIOPowerId() {
          PowerOperate.getInstance().enableRfId();
      }
      
    
      /**
       * 打开info电源
       */
      public void openGPIOPowerInfo() {
          PowerOperate.getInstance().enableRfInfo();
      }
    
      /**
       * 关闭电源
       */
      public void closeGPIOPower() {
          PowerOperate.getInstance().disableGPIO();
      }
    
      /**
       * 读取身份证id
       */
      public void readIDCardId() {
          CardHelper.getCardId(getSerialPort(), 30, new ReadIdResult() {
              @Override
              public void onSuccess(String cardId) {
                  //成功
              }
    
              @Override
              public void onFailure(int errorMessage) {
                  //失败
              }
          });
      }
    
      /**
       * 读取身份证信息
       */
      public void readIDCardInfo() {
          CardHelper.getCardInfo(getSerialPort(), 30, new ReadInfoResult() {
              @Override
              public void onSuccess(IDCard idCard) {
                  //成功
              }
    
              @Override
              public void onFailure(int errorMessage) {
                  //失败
              }
    
              @Override
              public void onFindCardSuccess() {
                  //寻卡成功
              }
    
              @Override
              public void onSelectCardSuccess() {
                  //选卡成功
              }
          });
      }
```    
