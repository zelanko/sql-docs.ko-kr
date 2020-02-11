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
ms.openlocfilehash: f104f7a6395442484be15f1e72c849edbf11e74f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70152685"
---
# <a name="sql-server-http_storage_object"></a>SQL Server, HTTP_STORAGE_OBJECT
  **SQLServer: HTTP_STORAGE_OBJECT** 성능 개체는 Azure Storage 계정을 모니터링 하는 성능 카운터로 구성 됩니다. [Azure의 SQL Server 데이터 파일](../databases/sql-server-data-files-in-microsoft-azure.md) 기능을 사용 하면 Azure Storage blob에 데이터베이스 파일을 저장할 수 있습니다. 이 성능 개체는 각 Azure 스토리지 계정을 각각 다른 드라이브로 취급합니다.  
  
|카운터 이름|Description|  
|------------------|-----------------|  
|**읽기 바이트 수/초**|읽기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**쓰기 바이트 수/초**|쓰기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**총 바이트 수/초**|읽기 또는 쓰기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**읽기/초**|HTTP 스토리지의 초당 읽기 수입니다.|  
|**쓰기/초**|HTTP 스토리지의 초당 쓰기 수입니다.|  
|**전송/초**|HTTP 스토리지의 초당 읽기 및 쓰기 작업 수입니다.|  
|**평균 바이트/읽기**|읽기당 HTTP 스토리지에서 전송된 평균 바이트 수입니다.|  
|**평균 바이트/쓰기**|쓰기당 HTTP 스토리지에서 전송된 평균 바이트 수입니다.|  
|**평균 바이트/전송**|읽기 또는 쓰기 작업 중 HTTP 스토리지에서 전송되는 평균 바이트 수입니다.|  
|**평균 마이크로 초/읽기**|HTTP 스토리지에서 각 읽기를 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**평균 마이크로 초/쓰기**|HTTP 스토리지에서 각 쓰기를 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**평균 마이크로 초/전송**|HTTP 스토리지로 각 전송을 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**미해결 HTTP 저장소 i/o**|HTTP 스토리지에 대한 총 미해결 I/O 수입니다.|  
|**HTTP 스토리지 I/O Retry/sec**|HTTP 스토리지로 보낸 초당 재시도 요청 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
