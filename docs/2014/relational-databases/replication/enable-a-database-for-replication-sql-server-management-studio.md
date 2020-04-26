---
title: 데이터베이스 복제 설정(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f31471aceef4937ee34d6492605e3a98dbcd973b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721326"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>데이터베이스 복제 설정(SQL Server Management Studio)
  **sysadmin** 고정 서버 역할의 멤버가 새 게시 마법사로 게시를 만들면 데이터베이스가 복제를 사용할 수 있도록 암시적으로 설정됩니다. **db_owner** 고정 데이터베이스 역할의 멤버가 해당 데이터베이스에 하나 이상의 게시를 만들 수 있도록 **sysadmin** 고정 서버 역할의 멤버는 데이터베이스가 복제를 사용할 수 있도록 명시적으로 설정할 수도 있습니다. 데이터베이스를 명시적으로 사용하려면 **게시자 속성 - \<Publisher>** 대화 상자의 **게시 데이터베이스** 페이지를 사용합니다. 이 대화 상자에 액세스하는 방법은 [Create a Publication](publish/create-a-publication.md)을 참조하십시오.  
  
### <a name="to-enable-a-database-for-replication"></a>데이터베이스 복제를 설정하려면  
  
1.  **게시자 속성 - \<Publisher>** 대화 상자의 **게시 데이터베이스** 페이지에서 복제할 각 데이터베이스에 대해 **트랜잭션** 및/또는 **병합** 확인란을 선택합니다. 데이터베이스에서 스냅샷 복제를 설정하려면 **트랜잭션** 을 선택합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
