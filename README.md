# BP implementation



```
public class BPManager {
  // constructor
  public BPManager(Context context,BluetoothAdapter adapter) {
    ...
  }

  // start scanning function
  public void scanLeDevice(final boolean enable) {
    ...
  }

  // so i can use registerReceiver(BroadcastReceiver mGattUpdateReceiver, BPManager.makeGattUpdateIntentFilter())
  public static IntentFilter makeGattUpdateIntentFilter() {
    final IntentFilter intentFilter = new IntentFilter();
    intentFilter.addAction(BluetoothLeService.ACTION_GATT_CONNECTED);
    intentFilter.addAction(BluetoothLeService.ACTION_GATT_DISCONNECTED);
    intentFilter.addAction(BluetoothLeService.ACTION_DATA_AVAILABLE);

    intentFilter.addAction(ACTION_START_SCAN);
    return intentFilter;
}

}
```
