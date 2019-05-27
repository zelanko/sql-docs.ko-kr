---
title: 연결 매개 변수 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], connections
- authentication [Upgrade Advisor]
- SQL Server Upgrade Advisor, connections
- connections [Upgrade Advisor]
- server instances [Upgrade Advisor]
- default server instances
- analyzing system [Upgrade Advisor], connections
ms.assetid: f754d038-637a-4d8e-85b0-b242e6499d26
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca5d6ed8f1e8a92d22bd32e39c8afe946a0fcfee
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095976"
---
# <a name="connection-parameters"></a>연결 매개 변수
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]과 같은 특정 서버 유형을 분석하려면 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스가 자동으로 선택됩니다. 이 선택 항목을 변경할 수 있지만 업그레이드 관리자에서 분석할 인스턴스는 한 번에 하나만 선택할 수 있습니다. 인증이 필요한 서버 유형을 포함한 경우 인증 모드와 자격 증명을 입력해야 합니다.  
  
## <a name="options"></a>변수  
 **서버 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 창에 입력한 컴퓨터 이름으로 미리 채워집니다.  
  
 **인스턴스 이름**  
 컴퓨터에서 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 선택합니다. 인스턴스 목록이 표시되지 않으면 MSSQLSERVER를 사용하여 기본 인스턴스를 검색할 수 있습니다. 이 작업은 원격 컴퓨터와 특히 관련이 있습니다. "default"라는 단어를 사용하여 기본 인스턴스를 검색할 수도 있습니다.  
  
 **인증**  
 이 컴퓨터에서 사용할 수 있는 인증 모드 목록에서 선택합니다. 기본 인증 모드는 Windows 인증입니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 이 상자에 사용자 이름을 입력합니다. 컴퓨터에 대한 관리자 자격 증명이 있는 사용자 이름을 입력하는 것이 좋습니다.  
  
> [!NOTE]  
>  Windows 인증을 선택 하면 현재 로그온 한 사용자의 사용자 이름에 채워집니다 합니다 **사용자 이름** 입력란입니다.  
  
 **암호**  
 지정된 사용자의 암호를 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자를 사용 하 여 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [업그레이드 관리자 사용자 인터페이스 참조](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
