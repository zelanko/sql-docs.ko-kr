---
title: SQL Server 리소스 상태 문제 해결(SQL Server 유틸리티) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4a6ca39149d6b14276e4a98384f266bb666ed10d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68115546"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>SQL Server 리소스 상태 문제 해결(SQL Server 유틸리티)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에서 식별하는 리소스 상태 문제 해결에는 컴퓨터 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 사용 과다 CPU의 완화 또는 데이터 계층 애플리케이션에 대한 사용 과다 CPU 완화가 포함될 수 있습니다. 그 밖의 문제로는 데이터베이스 파일에 대한 사용 과다 공간을 해결하거나 스토리지 볼륨에 할당된 디스크 공간의 사용 과다 문제를 해결하는 것 등이 있습니다.  
  
 데이터베이스가 "응급" 상태인 경우 상태에는 사용 과다 상태의 로그 파일 공간이 표시됩니다.  
  
 UCP의 관리되는 인스턴스 목록 뷰에 회색 상태 아이콘으로 표시되는 데이터 수집 실패에 대한 자세한 내용은 [SQL Server 유틸리티 문제 해결](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)을 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 시작에 대한 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에서 식별하는 특정 리소스 상태 문제를 완화하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [SQL Server 버전 및 에디션 확인 방법](https://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [SQL Server 2008의 성능 문제 해결](https://go.microsoft.com/fwlink/?LinkId=151354)  
  
  
