---
title: SQL Server, HTTP_STORAGE_OBJECT | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a33585b216da10bd09a604905c50ce97b528de49
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52752855"
---
# <a name="sql-server-httpstorageobject"></a>SQL Server, HTTP_STORAGE_OBJECT
  **SQLServer:HTTP_STORAGE_OBJECT** 성능 개체는 Microsoft Azure Storage 계정을 모니터링하는 성능 카운터로 구성됩니다. 사용 하 여 [Windows Azure의 SQL Server 데이터 파일](../databases/sql-server-data-files-in-microsoft-azure.md) 기능을 Windows Azure Storage Blob에 데이터베이스 파일을 저장할 수 있습니다. 이 성능 개체는 각 Windows Azure 스토리지 계정을 다른 드라이브로 처리합니다.  
  
|카운터 이름|Description|  
|------------------|-----------------|  
|**Read Bytes/sec**|읽기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**Write Bytes/sec**|쓰기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**Total Bytes/sec**|읽기 또는 쓰기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**읽기/초**|HTTP 스토리지의 초당 읽기 수입니다.|  
|**쓰기/초**|HTTP 스토리지의 초당 쓰기 수입니다.|  
|**Transfers/sec**|HTTP 스토리지의 초당 읽기 및 쓰기 작업 수입니다.|  
|**Avg. Bytes/Read**|읽기당 HTTP 스토리지에서 전송된 평균 바이트 수입니다.|  
|**Avg. Bytes/Write**|쓰기당 HTTP 스토리지에서 전송된 평균 바이트 수입니다.|  
|**Avg. Bytes/Transfer**|읽기 또는 쓰기 작업 중 HTTP 스토리지에서 전송되는 평균 바이트 수입니다.|  
|**Avg. microsec/Read**|HTTP 스토리지에서 각 읽기를 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**Avg. microsec/Write**|HTTP 스토리지에서 각 쓰기를 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**Avg. microsec/Transfer**|HTTP 스토리지로 각 전송을 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**Outstanding HTTP Storage I/O**|HTTP 스토리지에 대한 총 미해결 I/O 수입니다.|  
|**HTTP Storage I/O Retry/sec**|HTTP 스토리지로 보낸 초당 재시도 요청 수입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
