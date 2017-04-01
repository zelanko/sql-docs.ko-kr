---
title: "배포자에서 원격 게시자 설정(SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "원격 배포자 [SQL Server 복제]"
  - "게시자 [SQL Server 복제]"
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 배포자에서 원격 게시자 설정(SQL Server Management Studio)
  **게시자** 페이지에서 원격 배포자를 사용하려면 게시자를 설정합니다. 이 페이지는 배포 구성 마법사에서 사용할 수 있는 고 **배포자 속성-\< 배포자>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md) 및 [보기 및 수정 게시자 및 배포자 속성](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)합니다.  
  
### 배포 구성 마법사에서 게시자를 설정하려면  
  
1.  배포 구성 마법사의 **게시자** 페이지에서 **추가**를 클릭합니다.  
  
2.  **SQL Server 게시자 추가**를 클릭합니다. 배포자를 사용하도록 Oracle 게시자를 설정하는 방법은 [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)를 참조하십시오.  
  
3.  **서버에 연결** 대화 상자에서 원격 배포자를 사용할 게시자에 대한 연결 정보를 지정한 다음 **연결**을 클릭합니다.  
  
4.  에 **배포자 암호** 페이지는 **암호** 및 **암호 확인** 텍스트 상자에 대 한 강력한 암호를 지정는 **distributor_admin** 계정 복제 관리 작업을 수행 하기 위해 배포자에 게시자에서 연결에 사용 합니다.  
  
5.  를 확인 하 고 게시자에 대 한 설정을 수정 속성 단추를 클릭 (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### 배포자 속성 대화 상자에서 게시자를 설정하려면  
  
1.  에 **게시자** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자를 클릭 하 여 **추가**합니다.  
  
2.  **SQL Server 게시자 추가**를 클릭합니다. 배포자를 사용하도록 Oracle 게시자를 설정하는 방법은 [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)를 참조하십시오.  
  
3.  **서버에 연결** 대화 상자에서 원격 배포자를 사용할 게시자에 대한 연결 정보를 지정한 다음 **연결**을 클릭합니다.  
  
4.  에 **게시자** 페이지는 **암호** 및 **암호 확인** 텍스트 상자에 대 한 강력한 암호를 지정는 **distributor_admin** 계정 복제 관리 작업을 수행 하기 위해 배포자에 게시자에서 연결에 사용 합니다.  
  
5.  를 확인 하 고 게시자에 대 한 설정을 수정 속성 단추를 클릭 (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 참고 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [배포자 보안 설정](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  