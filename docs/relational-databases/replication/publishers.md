---
description: 게시자
title: 게시자 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.enablepublishers.f1
ms.assetid: 116cd6a5-32ac-4273-81a2-d184408e0f07
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 6aa802cc14b494a3892fea71d2ddbc99f42c8749
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479834"
---
# <a name="publishers"></a>게시자
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  다른 게시자에 이 배포자를 사용하도록 사용 권한을 지정할 수 있습니다. 현재 서버를 원격 배포자로 사용하도록 게시자를 설정해도 해당 서버가 게시자가 되지는 않습니다. 게시자에 연결하여 이를 게시자로 구성하고, 이 서버를 배포자로 선택해야 합니다. 새 게시 마법사를 통해 게시자를 구성하고 배포자를 선택할 수 있습니다.  
  
 게시자로 선택한 서버는 이 마법사의 **배포 데이터베이스** 페이지에서 지정한 배포 데이터베이스를 사용합니다. 다른 배포 데이터베이스를 사용하려면 이때 게시자를 설정하지 마십시오. 대신 배포 구성 마법사를 완료한 후 **배포자 속성** 대화 상자를 사용하여 게시자를 추가합니다.  
  
## <a name="options"></a>옵션  
 **게시자**  
 이 배포자를 사용하도록 허용할 서버를 선택합니다. 게시자 옆의 속성 단추 ( **...** )를 클릭하여 추가 속성을 보고 설정할 수 있습니다.  
  
 **추가**  
 허용할 서버가 나열되지 않으면 **추가** 를 클릭하여 사용 가능한 게시자 목록에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자 또는 Oracle 게시자를 추가합니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
