---
title: SQL Server 복제 설치 | Microsoft Docs
description: SQL Server 설치 마법사를 사용하거나 명령 프롬프트 창에서 복제 구성 요소를 설치합니다.
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e5635065e77921b661d5b60e5ebcd0aad850295b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883492"
---
# <a name="install-sql-server-replication"></a>SQL Server 복제 설치

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

복제 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사 또는 명령 프롬프트를 사용하여 설치할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 설치할 때나 기존 인스턴스를 수정할 때 복제를 설치할 수 있습니다.  
  
복제 구성 요소를 설치한 후에는 복제를 사용하기 전에 먼저 서버를 구성해야 합니다. 자세한 내용은 [온라인 설명서의](../../relational-databases/replication/configure-distribution.md) 배포 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
>[!IMPORTANT]  
>기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 수정할 때 복제 구성 요소를 설치하는 경우 설치가 완료된 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 중지하고 다시 시작해야 합니다. 이 동작을 수행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 복제 에이전트 하위 시스템을 인식하며 작업 단계에서 복제 에이전트를 호출할 수 있습니다.  
  
## <a name="installing-replication-by-using-setup"></a>설치 프로그램을 사용하여 복제 설치  
**다음의 새 인스턴스를 설치할 때 복제를 설치하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- RMO(복제 관리 개체)를 비롯한 복제 구성 요소를 설치하려면 설치 마법사의 **기능 선택** 페이지에서 **SQL Server 복제** 를 선택합니다.  
  
## <a name="installing-replication-from-the-command-prompt"></a>명령 프롬프트에서 복제 설치  
 **다음의 새 인스턴스를 설치할 때 복제를 설치하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치](../../database-engine/install-windows/install-sql-server.md)   
 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [SQL Server 버전에서 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
  
