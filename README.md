# BP implementation


What i'll do :
--------------
```
private void initBP(){
    if (!getPackageManager().hasSystemFeature(PackageManager.FEATURE_BLUETOOTH_LE)) {
        Toast.makeText(this, "BLE is not supported", Toast.LENGTH_SHORT).show();
    }

    final BluetoothManager bluetoothManager =
            (BluetoothManager) getSystemService(Context.BLUETOOTH_SERVICE);
    mBluetoothAdapter = bluetoothManager.getAdapter();
    // 检查设备上是否支持蓝牙
    if (mBluetoothAdapter == null) {
        Toast.makeText(this, "error bluetooth not supported", Toast.LENGTH_SHORT).show();
    }else{
        mBluetoothAdapter.enable();
        mManager = new BPManager(this, mBluetoothAdapter);
    }
}
```
i'll then call :
```
registerReceiver(mGattUpdateReceiver, BLEManager.makeGattUpdateIntentFilter());
mManager.scanLeDevice(true);
```

where i can handle event like that :
```
public final BroadcastReceiver mGattUpdateReceiver = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
        final String action = intent.getAction();
        if (BluetoothLeService.ACTION_GATT_CONNECTED.equals(action)) {
            Toast.makeText(CheckUpActivity.this, R.string.connected, Toast.LENGTH_SHORT).show();
        }  else if (BluetoothLeService.ACTION_GATT_DISCONNECTED.equals(action)) {
          if(mManager!=null){
              mManager.closeService();
          }
          Toast.makeText(CheckUpActivity.this, R.string.disconnected, Toast.LENGTH_SHORT).show();
        }
    }
}
```
so i can get data in ACTION_DATA_AVAILABLE event

What you need to do :
---------------------

- Modify existing example, you don't want an onCreate() method which will call scanLeDevice(true) because i'll
call it by myself.
- auto-connect to bioland-BPM in onLeScan() callback. (i already started a bit this part)
- send back the result with the broadcast at ACTION_DATA_AVAILABLE.
