# 鍒嗗竷寮忚兘鍔涳紙Distributed Kit锛?
> **閫傜敤鐗堟湰**锛欻armonyOS 6.1 / API 23锛堢ǔ瀹氾級銆傚吋瀹?API 14+銆?
## 姒傝堪

DistributedKit 鎻愪緵璁惧鍙戠幇銆佽澶囪縼绉伙紙Continuation锛夈€佽法璁惧鍓创鏉裤€佽法璁惧鎷栨嫿銆佸垎甯冨紡鏁版嵁鍚屾绛夎兘鍔涳紝鏄疄鐜?HarmonyOS "1+8+N" 鍏ㄥ満鏅崗鍚岀殑鏍稿績宸ュ叿闆嗐€?
## 璁惧鍙戠幇

### 璁惧绠＄悊

```typescript
import { deviceManager } from '@kit.DistributedKit';
import { BusinessError } from '@kit.BasicServicesKit';

let dmInstance: deviceManager.DeviceManager | undefined = undefined;

deviceManager.createDeviceManager('com.example.myapp', (err, data) => {
  if (err) {
    console.error('Create device manager failed: ' + err.message);
    return;
  }
  dmInstance = data;
  console.info('Device manager created.');
});
```

### 鑾峰彇鍙俊璁惧鍒楄〃

```typescript
if (dmInstance) {
  let deviceList: Array<deviceManager.DeviceInfo> = dmInstance.getTrustedDeviceListSync();
  deviceList.forEach(device => {
    console.info('Device: ' + device.deviceName + ', ID: ' + device.deviceId + ', Type: ' + device.deviceType);
  });
}
```

### 鍙戠幇鍛ㄨ竟璁惧

```typescript
if (dmInstance) {
  dmInstance.on('deviceFound', (data: deviceManager.DeviceDiscoverEvent) => {
    console.info('Found device: ' + data.device.deviceName);
  });

  dmInstance.on('discoverFail', (data: deviceManager.DiscoverFailEvent) => {
    console.error('Discover failed: ' + data.reason);
  });

  let discoverParam: Record<string, string> = {
    'discoverTargetType': '1'
  };
  let filterOptions: Record<string, string> = {
    'targetType': '1',
    'availableStatus': '0'
  };

  dmInstance.startDiscovering(discoverParam, filterOptions);
}
```

### 鍋滄鍙戠幇

```typescript
if (dmInstance) {
  dmInstance.stopDiscovering();
  dmInstance.off('deviceFound');
  dmInstance.off('discoverFail');
}
```

## 璁惧杩佺Щ锛圕ontinuation锛?
### 澹版槑杩佺Щ鑳藉姏

```json5
// module.json5
{
  "module": {
    "abilities": [
      {
        "name": "EntryAbility",
        "continuable": true
      }
    ]
  }
}
```

### 鍙戣捣杩佺Щ

```typescript
import { AbilityConstant, UIAbility } from '@kit.AbilityKit';
import { deviceManager } from '@kit.DistributedKit';

class EntryAbility extends UIAbility {
  onContinue(wantParam: Record<string, Object>): AbilityConstant.OnContinueResult {
    let userData: Record<string, string> = {
      'currentPage': 'detail',
      'itemId': '12345'
    };
    wantParam['userData'] = JSON.stringify(userData);
    console.info('onContinue called.');
    return AbilityConstant.OnContinueResult.AGREE;
  }

  onCreate(want, launchParam): void {
    if (launchParam.launchReason === AbilityConstant.LaunchReason.CONTINUATION) {
      let userData = JSON.parse(wantParam['userData'] as string);
      console.info('Restored page: ' + userData.currentPage);
    }
  }
}
```

### 杩佺Щ瀹屾垚鍥炶皟

```typescript
class EntryAbility extends UIAbility {
  onContinue(wantParam: Record<string, Object>): AbilityConstant.OnContinueResult {
    wantParam['userData'] = JSON.stringify({ key: 'value' });
    return AbilityConstant.OnContinueResult.AGREE;
  }

  onRestoreData(wantParam: Record<string, Object>): void {
    let restoredData = JSON.parse(wantParam['userData'] as string);
    console.info('Restore data: ' + JSON.stringify(restoredData));
  }
}
```

## 璺ㄨ澶囧壀璐存澘

```typescript
import { pasteboard } from '@kit.BasicServicesKit';
import { distributedDeviceManager } from '@kit.DistributedKit';

let systemPasteboard = pasteboard.getSystemPasteboard();

let pasteData = pasteboard.createData(pasteboard.MIMETYPE_TEXT_PLAIN, 'Cross-device text');

let property: pasteboard.PasteDataProperty = {
  localOnly: false
};
pasteData.setProperty(property);

systemPasteboard.setData(pasteData, (err) => {
  if (err) {
    console.error('Set cross-device pasteboard failed: ' + err.message);
    return;
  }
  console.info('Cross-device pasteboard data set.');
});
```

## 璺ㄨ澶囨嫋鎷?
```typescript
import { UDMF } from '@kit.UnifiedDataManagementKit';
import { distributedDeviceManager } from '@kit.DistributedKit';

let unifiedData = new UDMF.UnifiedData();
let plainText = new UMDF.PlainText();
plainText.textContent = 'Drag across devices';
unifiedData.addRecord(plainText);

let dragInfo: DragInfo = {
  data: unifiedData,
  targetDevices: ['remote_device_id_1']
};
```

## 鍒嗗竷寮忔暟鎹悓姝?
### 鍒嗗竷寮忛敭鍊兼暟鎹簱

```typescript
import { distributedKVStore } from '@kit.ArkData';
import { BusinessError } from '@kit.BasicServicesKit';

let kvManager: distributedKVStore.KVManager | undefined = undefined;

let kvManagerConfig: distributedKVStore.KVManagerConfig = {
  bundleName: 'com.example.myapp',
  context: getContext(this)
};

kvManager = distributedKVStore.createKVManager(kvManagerConfig);

let kvStore: distributedKVStore.SingleKVStore | undefined = undefined;

let storeOptions: distributedKVStore.Options = {
  createIfMissing: true,
  encrypt: false,
  backup: false,
  autoSync: true,
  kvStoreType: distributedKVStore.KVStoreType.SINGLE_VERSION,
  securityLevel: distributedKVStore.SecurityLevel.S2
};

kvManager.getKVStore('distributed_store', storeOptions, (err, store) => {
  if (err) {
    console.error('Get KV store failed: ' + err.message);
    return;
  }
  kvStore = store;
  console.info('KV store created.');
});
```

### 鍐欏叆涓庡悓姝ユ暟鎹?
```typescript
if (kvStore) {
  kvStore.put('sync_key', 'sync_value', (err) => {
    if (err) {
      console.error('Put data failed: ' + err.message);
      return;
    }
    console.info('Put data succeeded.');
  });

  kvStore.on('dataChange', distributedKVStore.ChangeType.SUBSCRIBE_TYPE_ALL, (data) => {
    console.info('Data changed: ' + JSON.stringify(data));
  });
}
```

### 鎵嬪姩鍚屾

```typescript
import { deviceManager } from '@kit.DistributedKit';

if (kvStore) {
  let deviceList = dmInstance.getTrustedDeviceListSync();
  let deviceIds = deviceList.map(device => device.deviceId);

  kvStore.sync(deviceIds, distributedKVStore.SyncMode.PUSH_PULL, 1000);
}
```

## 鏉冮檺

| 鏉冮檺 | 璇存槑 |
|------|------|
| `ohos.permission.DISTRIBUTED_DATASYNC` | 鍒嗗竷寮忔暟鎹悓姝?|
| `ohos.permission.ACCESS_SERVICE_DM` | 璁惧绠＄悊 |
| `ohos.permission.DISTRIBUTED_SOFTBUS_CENTER` | 鍒嗗竷寮忚蒋鎬荤嚎 |

---

## 瀹樻柟鍙傝€?
- 鍒嗗竷寮忚兘鍔涙杩帮細https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/distributed-overview-V5
- 璁惧鍙戠幇锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/device-discovery-V5
- 璁惧杩佺Щ锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/continuation-V5
- 鍒嗗竷寮忔暟鎹悓姝ワ細https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/distributed-data-sync-V5
- deviceManager API锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-device-manager-V5
- distributedKVStore API锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-distributedkvstore-V5