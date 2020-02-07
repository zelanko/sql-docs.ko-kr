---
title: SQL Server, HTTP_STORAGE_OBJECT | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 6ce8040b37ec08c82b11c9ff572c13125064523b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70155774"
---
# <a name="sql-server-http-storage"></a>SQL Server, HTTP 스토리지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:HTTP Storage** 성능 개체는 Microsoft Azure Storage 계정을 모니터링하는 성능 카운터로 구성됩니다. [Microsoft Azure의 SQL Server 데이터 파일](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) 기능을 사용하여 Azure Storage Blob에 데이터베이스 파일을 저장할 수 있습니다. 이 성능 개체는 각 Azure 스토리지 계정을 각각 다른 드라이브로 취급합니다.  
  
|카운터 이름|Description|  
|------------------|-----------------|  
|**Avg. Bytes/Read**|읽기당 HTTP 스토리지에서 전송된 평균 바이트 수입니다.|  
|**Avg. Bytes/Transfer**|읽기 또는 쓰기 작업 중 HTTP 스토리지에서 전송되는 평균 바이트 수입니다.|  
|**Avg. Bytes/Write**|쓰기당 HTTP 스토리지에서 전송된 평균 바이트 수입니다.|  
|**Avg. microsec/Read**|HTTP 스토리지에서 각 읽기를 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**Avg. microsec/Read Comp**|HTTP에서 스토리지에 대한 읽기 작업을 완료하는 데 소요되는 평균 마이크로초의 수입니다.| 
|**Avg. microsec/Transfer**|HTTP 스토리지로 각 전송을 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**Avg. microsec/Write**|HTTP 스토리지에서 각 쓰기를 수행하는 데 걸리는 평균 마이크로초 수입니다.|  
|**Avg. microsec/Write Comp**|HTTP에서 스토리지에 대한 쓰기 작업을 완료하는 데 소요되는 평균 마이크로초의 수입니다.|  
|**HTTP 스토리지 IO failed/sec**|초당 HTTP 스토리지로 보내진 실패한 쓰기 요청의 수입니다.| 
|**HTTP 스토리지 I/O retry/sec**|HTTP 스토리지로 보낸 초당 재시도 요청 수입니다.|  
|**Outstanding HTTP 스토리지 I/O**|HTTP 스토리지에 대한 총 미해결 I/O 수입니다.|  
|**Read Bytes/sec**|읽기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**읽기/초**|HTTP 스토리지의 초당 읽기 수입니다.|  
|**Total Bytes/sec**|읽기 또는 쓰기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**Transfers/sec**|HTTP 스토리지의 초당 읽기 및 쓰기 작업 수입니다.|  
|**Write Bytes/sec**|쓰기 작업 중 HTTP 스토리지에서 초당 전송되는 데이터의 양입니다.|  
|**쓰기/초**|HTTP 스토리지의 초당 쓰기 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
