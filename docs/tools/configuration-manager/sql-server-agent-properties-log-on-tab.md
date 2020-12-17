---
title: SQL Server 에이전트 속성(로그온 탭)
description: SQL Server 에이전트 속성 대화 상자의 로그온 탭에 대해 알아봅니다. 이 탭을 사용하여 계정을 지정하고 서비스를 시작 또는 중지하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 01fc6329-5d6b-4186-9565-395f375477bb
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: fec249633ad0edb6e925afc2a67ee8a6bbecf629
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483775"
---
# <a name="sql-server-agent-properties-log-on-tab"></a>SQL Server 에이전트 속성(로그온 탭)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  **SQL Server 에이전트 속성** 대화 상자의 **로그온** 탭을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에서 사용할 계정을 지정할 수 있으며 서비스를 시작 및 중지할 수 있습니다. 계정의 암호를 변경하면 서비스를 다시 시작하지 않고 즉시 적용됩니다.  
  
> [!NOTE]  
>  클러스터형 인스턴스의 서비스에서 사용하는 계정 이름을 변경하는 경우 새 계정은 변경되는 서비스의 설치 중에 지정한 도메인 그룹의 멤버여야 합니다. 그렇지 않으면 해당 그룹에 멤버를 추가할 수 있는 권한이 있어야 합니다. 그룹 멤버 자격을 수정할 권한이 없을 경우 도메인 관리자에게 문의하십시오.  
  
## <a name="options"></a>옵션  
 **로컬 시스템 계정**  
 암호를 요구하지 않는 로컬 시스템 계정을 지정합니다. 그러나 로컬 시스템 계정은 계정에 부여된 권한에 따라 다른 서버와 상호 작용하지 못하도록 서비스를 제한할 수 있습니다.  
  
 **계정 지정**  
 Windows 인증을 사용하는 로컬 또는 도메인 사용자 계정을 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 서비스에 대해 최소의 권한을 가진 도메인 사용자 계정을 사용할 것을 권장합니다. 계정 선택 방법은 온라인 설명서의 "Windows 서비스 계정 설정"을 참조하십시오.  
  
 **계정 이름**  
 로컬 또는 도메인 사용자 계정 이름을 지정합니다.  
  
 **암호**  
 계정의 암호를 입력합니다.  
  
 **암호 확인**  
 계정의 암호를 다시 입력합니다.  
  
 **시작**  
 서비스를 시작합니다.  
  
 **중지**  
 서비스를 중지합니다.  
  
 **일시 중지**  
 서비스를 일시 중지합니다.  
  
 **재개**  
 일시 중지한 서비스를 다시 시작합니다.  
  
  
