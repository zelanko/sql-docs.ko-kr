---
title: NVDIMM-N 쓰기 저장 캐시를 사용하여 스토리지 공간 구성 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 861862fa-9900-4ec0-9494-9874ef52ce65
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: c7d2e9a53d002013551e24d2aaa0ff70bc266772
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328274"
---
# <a name="configuring-storage-spaces-with-a-nvdimm-n-write-back-cache"></a>NVDIMM-N 쓰기 저장 캐시를 사용하여 스토리지 공간 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Windows Server 2016은 매우 빠르게 I/O(입출력) 작업을 수행할 수 있는 NVDIMM-N 디바이스를 지원합니다. 이러한 디바이스를 사용하는 좋은 방법 중 하나는 쓰기 대기 시간을 짧게 하는 쓰기 저장 캐시입니다. 이 항목에서는 SQL Server 트랜잭션 로그를 저장할 가상 드라이브로 미러된 NVDIMM-N 쓰기 저장 캐시를 사용하여 미러된 스토리지 공간을 설정하는 방법을 설명합니다. 또한 데이터 테이블 또는 기타 데이터를 저장하는 데 사용하려는 경우 스토리지 풀에 더 많은 디스크를 포함하거나 격리가 중요한 경우 여러 풀을 만들 수 있습니다.  
  
 이 기술을 사용하는 Channel 9 비디오를 보려면 [Using Non-volatile Memory (NVDIMM-N) as Block Storage in Windows Server 2016](https://channel9.msdn.com/Events/Build/2016/P466)(Windows Server 2016에서 블록 스토리지로 비휘발성 메모리(NVDIMM-N) 사용)를 참조하세요.  
  
## <a name="identifying-the-right-disks"></a>올바른 디스크 식별  
 Windows Server 2016에서 스토리지 공간 설정, 특히 쓰기 저장 캐시와 같은 고급 기능을 사용한 설정은 PowerShell을 통해 가장 쉽게 수행됩니다. 첫 번째 단계는 가상 디스크가 생성될 스토리지 공간 풀이 있어야 하는 디스크를 식별하는 것입니다. NVDIMM-N에는 SCM(스토리지 클래스 메모리)의 버스 유형 및 미디어 유형이 있는데 Get-PhysicalDisk PowerShell cmdlet을 통해 쿼리할 수 있습니다.  
  
```  
Get-PhysicalDisk | Select FriendlyName, MediaType, BusType  
```  
  
 ![Get-PhysicalDisk](../../relational-databases/performance/media/get-physicaldisk.png "Get-PhysicalDisk")  
  
> [!NOTE]  
>  NVDIMM-N 디바이스에서는 더 이상 쓰기 저장 캐시 대상이 될 수 있는 디바이스를 특별히 선택하지 않아도 됩니다.  
  
 미러된 쓰기 저장 캐시로 미러된 가상 디스크를 만들려면 적어도 2개의 NVDIMM-N 및 다른 2개의 디스크가 필요합니다. 풀을 빌드하기 전에 원하는 실제 디스크를 변수에 할당하면 프로세스가 더 쉬워집니다.  
  
```  
$pd =  Get-PhysicalDisk | Select FriendlyName, MediaType, BusType | WHere-Object {$_.FriendlyName -like 'MK0*' -or $_.FriendlyName -like '2c80*'}  
```  
  
 이 스크린샷은 다음 PowerShell cmdlet을 사용하여 반환되도록 할당된 $pd 변수와 2개의 SSD 및 2개의 NVDIMM-N을 보여 줍니다.  
  
```  
$pd | Select FriendlyName, MediaType, BusType  
```  
  
 ![FriendlyName 선택](../../relational-databases/performance/media/select-friendlyname.png "FriendlyName 선택")  
  
## <a name="creating-the-storage-pool"></a>스토리지 풀 만들기  
 PhysicalDisks를 포함하는 $pd 변수를 사용하면 New-StoragePool PowerShell cmdlet을 사용하여 스토리지 풀을 쉽게 빌드할 수 있습니다.  
  
```  
New-StoragePool -StorageSubSystemFriendlyName "Windows Storage*" -FriendlyName NVDIMM_Pool -PhysicalDisks $pd  
```  
  
 ![New-StoragePool](../../relational-databases/performance/media/new-storagepool.png "New-StoragePool")  
  
## <a name="creating-the-virtual-disk-and-volume"></a>가상 디스크 및 볼륨 만들기  
 이제 풀을 만들었으며 다음 단계는 가상 디스크를 지정하고 서식을 지정하는 것입니다. 이 경우 하나의 가상 디스크만 만들어지고 New-Volume PowerShell cmdlet을 사용하여 이 프로세스를 간소화할 수 있습니다.  
  
```  
New-Volume -StoragePool (Get-StoragePool -FriendlyName NVDIMM_Pool) -FriendlyName Log_Space -Size 300GB -FileSystem NTFS -AccessPath S: -ResiliencySettingName Mirror  
```  
  
 ![New-Volume](../../relational-databases/performance/media/new-volume.png "New-Volume")  
  
 가상 디스크가 만들어지고 초기화되며 NTFS로 포맷됩니다. 아래 화면 캡처에서 가상 디스크 크기는 300GB, 쓰기 캐시 크기는 1GB로, NVDIMM-N에서 호스트됩니다.  
  
 ![Get-virtualdisk](../../relational-databases/performance/media/get-virtualdisk.png "Get-virtualdisk")  
  
 이제 서버에 이 새 볼륨이 표시되는 것을 볼 수 있습니다. 이제 SQL Server 트랜잭션 로그에 이 드라이브를 사용할 수 있습니다.  
  
 ![Log_Space 드라이브](../../relational-databases/performance/media/log-space-drive.png "Log_Space 드라이브")  
  
## <a name="see-also"></a>참고 항목  
 [Windows 10에서 Windows 저장소 공간](https://windows.microsoft.com/windows-10/storage-spaces-windows-10)   
 [Windows 2012 R2에서 Windows 저장소 공간](https://technet.microsoft.com/library/hh831739.aspx)   
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [데이터 및 로그 파일의 기본 위치 보기 또는 변경&#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)  
  
  
