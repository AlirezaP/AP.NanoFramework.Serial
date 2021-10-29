# AP.NanoFramework.Serial

A Helper For Work With Serial (UART) in nanoframework.

Sample:

            // COM2 in ESP32-WROVER-KIT mapped to free GPIO pins
            // mind to NOT USE pins shared with other devices, like serial flash and PSRAM
            // also it's MANDATORY to set pin function to the appropriate COM before instantiating it
            // set GPIO functions for COM2 (this is UART1 on ESP32)

            Configuration.SetPinFunction(17, DeviceFunction.COM2_TX);
            Configuration.SetPinFunction(16, DeviceFunction.COM2_RX);

            _gsmSerialDevice = SerialDevice.FromId("COM2");
            _gsmSerialDevice.BaudRate = 9600;// 9600;
            _gsmSerialDevice.Parity = SerialParity.None;
            _gsmSerialDevice.StopBits = SerialStopBitCount.One;
            _gsmSerialDevice.Handshake = SerialHandshake.None;
            _gsmSerialDevice.DataBits = 8;

            _apSerialHelper = new AP.NanoFrameWork.Serial.SerialHelper(_gsmSerialDevice);
            
            _serialHelper.DataRecivedEventHandler += _serialHelper_DataRecivedEventHandler;
            
            _serialHelper.WriteToSerial("some data1", "ok", true, true);
            _serialHelper.WriteToSerial("some data2", "ok");
            _serialHelper.WriteToSerial("some data3");
            
            
        private void _serialHelper_DataRecivedEventHandler(object source, Serial.SerialHelper.MyEventArgs e)
        {


            string dataRecived = e.GetInfo();

            Debug.WriteLine("from Event: " + dataRecived + " End event");
            
        }
            '

'
