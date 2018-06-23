---
title: SQL Server 리소스 상태 문제 해결(SQL Server 유틸리티) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f8769802f30f83541d853bf354eb46dc3288590b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078588"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>SQL Server 리소스 상태 문제 해결(SQL Server 유틸리티)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에서 식별하는 리소스 상태 문제 해결에는 컴퓨터 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 사용 과다 CPU의 완화 또는 데이터 계층 응용 프로그램에 대한 사용 과다 CPU 완화가 포함될 수 있습니다. 그 밖의 문제로는 데이터베이스 파일에 대한 사용 과다 공간을 해결하거나 저장소 볼륨에 할당된 디스크 공간의 사용 과다 문제를 해결하는 것 등이 있습니다.  
  
 데이터베이스가 "응급" 상태인 경우 상태에는 사용 과다 상태의 로그 파일 공간이 표시됩니다.  
  
 UCP의 관리되는 인스턴스 목록 뷰에 회색 상태 아이콘으로 표시되는 데이터 수집 실패에 대한 자세한 내용은 [SQL Server 유틸리티 문제 해결](../../database-engine/troubleshoot-the-sql-server-utility.md)을 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 시작에 대한 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에서 식별하는 특정 리소스 상태 문제를 완화하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [SQL Server 버전 및 에디션 확인 방법](http://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [SQL Server 2008의 성능 문제 해결](http://go.microsoft.com/fwlink/?LinkId=151354)  
  
  