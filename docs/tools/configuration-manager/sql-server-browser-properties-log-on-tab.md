---
title: SQL Server Browser 속성(로그온 탭)
description: SQL Server Browser 속성 대화 상자의 로그온 탭에 대해 알아봅니다. 이 탭을 사용하여 계정을 지정하고 서비스를 시작 또는 중지하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c77871ec-c2f4-4e4a-9a10-5aeb4ae70507
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 13c448b6f856b8c7027bcf044bc9fd8688533948
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897811"
---
# <a name="sql-server-browser-properties-log-on-tab"></a>SQL Server Browser 속성(로그온 탭)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 프로그램은 서버에서 서비스로 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스에 대해 들어오는 요청을 수신 대기하고 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 정보를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 UDP 포트에서 수신하고 SSRP( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol)를 사용하여 인증되지 않은 요청을 허용합니다.  
  
 계정의 암호를 변경하면 서비스를 다시 시작하지 않고 즉시 적용됩니다.  
  
## <a name="options"></a>옵션  
 **로컬 시스템 계정**  
 로컬 시스템 계정의 보안 컨텍스트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 실행합니다. 가능하면 이보다 낮은 권한의 계정을 사용하십시오.  
  
 **계정 지정**  
 Windows 인증을 사용하는 로컬 또는 도메인 사용자 계정을 지정합니다. 서비스에 대해 최소의 권한을 가진 도메인 사용자 계정을 사용하는 것이 좋습니다. 계정 선택 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "Windows 서비스 계정 설정"을 참조하십시오.  
  
 **찾아보기**  
 사용자 또는 기본 제공 보안 주체를 찾아봅니다.  
  
> [!IMPORTANT]  
>  낮은 권한의 계정을 사용하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스에 필요한 권한에 대한 자세한 내용은 [SQL Server Browser 서비스](../../tools/configuration-manager/sql-server-browser-service.md)의 보안 섹션을 참조하세요.  
  
 **암호**  
 보안 주체의 암호를 입력합니다.  
  
 **암호 확인**  
 보안 주체의 암호를 확인합니다.  
  
 **서비스 상태**  
 이 서비스가 실행 중인지, 중지되었는지 또는 비활성화되었는지 나타냅니다. “ **...** ”는 상태 변경이 보류 중임을 나타냅니다.  
  
 **시작**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 시작합니다.  
  
 **중지**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 중지합니다.  
  
 **일시 중지**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 일시 중지합니다.  
  
 **재개**  
 일시 중지한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 재개합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Browser 서비스](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
