---
title: FILESTREAM 사용 및 구성 | Microsoft Docs
description: FILESTREAM을 사용하려면 먼저 SQL Server 데이터베이스 엔진 인스턴스에서 FILESTREAM을 사용하도록 설정합니다. SQL Server 구성 관리자를 사용하여 FILESTREAM을 사용하도록 설정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], enabling
ms.assetid: 78737e19-c65b-48d9-8fa9-aa6f1e1bce73
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4e9e0fca818c4988acacfbfa89af718eda8d8ac5
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246587"
---
# <a name="enable-and-configure-filestream"></a>FILESTREAM 사용 및 구성

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  FILESTREAM을 사용하려면 먼저 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에서 FILESTREAM을 사용하도록 설정해야 합니다. 이 항목에서는 SQL Server 구성 관리자를 사용하여 FILESTREAM을 사용하도록 설정하는 방법에 대해 설명합니다.  
  
##  <a name="enabling-filestream"></a><a name="enabling"></a> FILESTREAM 설정  
  
#### <a name="to-enable-and-change-filestream-settings"></a>FILESTREAM을 사용하도록 설정하고 해당 설정을 변경하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  서비스 목록에서 **SQL Server 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **열기**를 클릭합니다.  
  
3.  **SQL Server 구성 관리자** 스냅인에서 FILESTREAM을 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 찾습니다.  
  
4.  해당 인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **SQL Server 속성** 대화 상자에서 **FILESTREAM** 탭을 클릭합니다.  
  
6.  **Transact-SQL 액세스에 FILESTREAM 사용** 확인란을 선택합니다.  
  
7.  Windows에서 FILESTREAM 데이터를 읽고 쓰려는 경우 **파일 I/O 스트리밍 액세스에 FILESTREAM 사용**을 클릭합니다. **Windows 공유 이름** 상자에 Windows 공유의 이름을 입력합니다.  
  
8.  원격 클라이언트가 이 공유에 저장된 FILESTREAM 데이터에 액세스해야 하는 경우 **원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스를 가질 수 있도록 허용**을 선택합니다.  
  
9. **적용**을 클릭합니다.  
  
10. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **새 쿼리** 를 클릭하여 쿼리 편집기를 표시합니다.  
  
11. 쿼리 편집기에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 입력합니다.  
  
    ```sql  
    EXEC sp_configure filestream_access_level, 2  
    RECONFIGURE  
    ```  
  
12. **실행**을 클릭합니다.  
  
13. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작합니다.  

##  <a name="best-practices"></a><a name="best"></a> 모범 사례  
  
###  <a name="physical-configuration-and-maintenance"></a><a name="config"></a> 물리적 구성 및 유지 관리  
 FILESTREAM 스토리지 볼륨을 설정할 때 다음 지침을 고려하십시오.  
  
-   FILESTREAM 컴퓨터 시스템에서 약식 파일 이름을 해제합니다. 약식 파일 이름은 생성하는 데 시간이 많이 소요됩니다. 약식 파일 이름을 비활성화하려면 Windows **fsutil** 유틸리티를 사용합니다.  
  
-   정기적으로 FILESTREAM 컴퓨터 시스템 조각 모음을 수행합니다.  
  
-   64KB NTFS 클러스터를 사용합니다. 압축된 볼륨은 4KB NTFS 클러스터로 설정해야 합니다.  
  
-   FILESTREAM 볼륨에서 인덱싱을 해제하고 **disablelastaccess**를 설정합니다. **disablelastaccess**를 설정하려면 Windows **fsutil** 유틸리티를 사용합니다.  
  
-   FILESTREAM 볼륨에 대한 바이러스 검사가 필요 없을 때는 해제합니다. 바이러스 검사가 필요한 경우, 잘못된 파일을 자동으로 삭제하는 정책을 설정하지 마십시오.  
  
-   애플리케이션에서 요구되는 내결함성 및 성능 RAID 수준을 설정하고 조절합니다.  
  
|RAID 수준|쓰기 성능|읽기 성능|내결함성|설명|  
|-|-|-|-|-|   
|RAID 5|정상|정상|최고|성능은 하나의 디스크 또는 JBOD보다 우수하지만 RAID 0 또는 스트라이프를 사용하는 RAID 5보다 떨어집니다.|  
|RAID 0|최고|최고|None||  
|RAID 5 + 스트라이프|최고|최고|최고|가장 비용이 많이 드는 옵션입니다.|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
  
###  <a name="physical-database-design"></a><a name="database"></a> 물리적 데이터베이스 디자인  
 FILESTREAM 데이터베이스를 디자인할 때 다음 같은 지침을 고려하십시오.  
  
-   FILESTREAM 열에는 해당하는 **uniqueidentifier**ROWGUID 열이 수반되어야 합니다. 이러한 종류의 테이블에는 고유한 인덱스도 함께 나타나야 합니다. 일반적으로 이러한 인덱스는 클러스터형 인덱스가 아닙니다. 데이터베이스 비즈니스 논리에 클러스터형 인덱스가 필요한 경우, 인덱스에 저장된 값이 임의의 값이 아니어야 합니다. 임의의 값인 경우에는 테이블에서 행이 추가되거나 제거될 때마다 인덱스가 다시 정렬됩니다.  
  
-   성능상의 이유로 FILESTREAM 파일 그룹 및 컨테이너는 운영 체제, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그, tempdb 또는 페이징 파일 이외의 볼륨에 있어야 합니다.  
  
-   공간 관리 및 정책은 FILESTREAM에서 직접적으로 지원되지 않습니다. 하지만 각 FILESTREAM 파일 그룹을 개별 볼륨에 지정하고 볼륨의 관리 기능을 사용하는 방법을 통해 간접적으로 공간을 관리하고 정책을 적용할 수 있습니다.  
  
  
