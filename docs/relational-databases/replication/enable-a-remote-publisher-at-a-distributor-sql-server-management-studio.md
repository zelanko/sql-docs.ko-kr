---
title: 배포자에서 원격 게시자 사용(SSMS)
description: SSMS(SQL Server Management Studio)를 사용하여 배포자에서 원격 게시자를 사용하도록 설정하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- remote Distributors [SQL Server replication]
- Publishers [SQL Server replication]
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: f5fa7595160176ec24f8106e5de71e59ea89eef3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85653275"
---
# <a name="enable-a-remote-publisher-at-a-distributor-sql-server-management-studio"></a>배포자에서 원격 게시자 설정(SQL Server Management Studio)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **게시자** 페이지에서 원격 배포자를 사용하려면 게시자를 설정합니다. 이 페이지는 배포 구성 마법사 및 **배포자 속성 - \<Distributor>** 대화 상자에서 사용할 수 있습니다. 마법사 사용 방법 및 대화 상자에 액세스하는 방법은 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md) 및 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
### <a name="to-enable-a-publisher-in-the-configure-distribution-wizard"></a>배포 구성 마법사에서 게시자를 설정하려면  
  
1.  배포 구성 마법사의 **게시자** 페이지에서 **추가**를 클릭합니다.  
  
2.  **SQL Server 게시자 추가**를 클릭합니다. 배포자를 사용하도록 Oracle 게시자를 설정하는 방법은 [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)를 참조하십시오.  
  
3.  **서버에 연결** 대화 상자에서 원격 배포자를 사용할 게시자에 대한 연결 정보를 지정한 다음 **연결**을 클릭합니다.  
  
4.  **배포자 암호** 페이지에서 **암호** 및 **암호 확인** 입력란에 관리 태스크를 수행하기 위해 게시자에서 배포자로 연결할 때 복제에서 사용하는 **distributor_admin** 계정에 대한 강력한 암호를 지정합니다.  
  
5.  게시자에 대한 설정을 보고 수정하려면 속성 단추( **...** )를 클릭합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

### <a name="to-enable-a-publisher-in-the-distributor-properties-dialog-box"></a>배포자 속성 대화 상자에서 게시자를 설정하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **게시자** 페이지에서 **추가**를 클릭합니다.  
  
2.  **SQL Server 게시자 추가**를 클릭합니다. 배포자를 사용하도록 Oracle 게시자를 설정하는 방법은 [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)를 참조하십시오.  
  
3.  **서버에 연결** 대화 상자에서 원격 배포자를 사용할 게시자에 대한 연결 정보를 지정한 다음 **연결**을 클릭합니다.  
  
4.  **게시자** 페이지에서 **암호** 및 **암호 확인** 입력란에 관리 태스크를 수행하기 위해 게시자에서 배포자로 연결할 때 복제에서 사용하는 **distributor_admin** 계정에 대한 강력한 암호를 지정합니다.  
  
5.  게시자에 대한 설정을 보고 수정하려면 속성 단추( **...** )를 클릭합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [배포자 보안 설정](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
