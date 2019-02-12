---
title: 인스턴스 구성 | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66329d4c25a23a6b3dbc3570723bab8aecfa3d4a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039884"
---
# <a name="instance-configuration"></a>인스턴스 구성
  **설치 마법사의** 인스턴스 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스를 만들지 또는 명명된 인스턴스를 만들지 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 아직 설치되지 않은 경우 명명된 인스턴스를 지정하지 않으면 기본 인스턴스가 만들어집니다.  
  
 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 특정 데이터 정렬과 기타 옵션이 지정된 고유의 서비스 집합으로 구성됩니다. 디렉터리 구조, 레지스트리 구조 및 서비스 이름은 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중 작성한 인스턴스 이름과 특정 인스턴스 ID를 반영합니다.  
  
 인스턴스는 기본 인스턴스이거나 명명된 인스턴스입니다. 기본 인스턴스 이름은 MSSQLSERVER입니다. 연결을 위해 클라이언트에서 인스턴스 이름을 지정할 필요는 없습니다. 명명된 인스턴스는 설치 중 사용자가 결정합니다. 기본 인스턴스를 먼저 설치하지 않고도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 명명된 인스턴스로 설치할 수 있습니다. 버전과 관계없이 한 번에 하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치만 기본 인스턴스가 될 수 있습니다.  
  
 **경고!** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep을 사용할 경우 **인스턴스 구성** 페이지에서 준비 인스턴스를 완료할 때 인스턴스 이름을 지정할 수 있습니다. 시스템에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기존 기본 인스턴스가 없는 경우 완료하려는 준비 인스턴스를 기본 인스턴스로 구성하도록 선택할 수 있습니다.  
  
## <a name="multiple-instances"></a>여러 인스턴스  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 단일 서버 또는 프로세서에서 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지원하지만 하나의 인스턴스만 기본 인스턴스가 될 수 있습니다. 다른 모든 인스턴스는 명명된 인스턴스여야 합니다. 한 컴퓨터에서 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 동시에 실행할 수 있으며 각 인스턴스는 다른 인스턴스와 독립적으로 실행됩니다.  
  
 자세한 내용은 [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 장애 조치(Failover) 클러스터 인스턴스만 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 클러스터 네트워크 이름을 지정합니다. 이 이름은 네트워크에서 장애 조치(Failover) 클러스터 인스턴스를 식별합니다.  
  
 기본 또는 명명된 인스턴스 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스 또는 명명된 인스턴스를 설치할지 결정할 때 다음 정보를 고려하십시오.  
  
-   데이터베이스 서버에 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치할 경우 이 인스턴스는 기본 인스턴스여야 합니다.  
  
-   동일한 컴퓨터에 여러 인스턴스를 설치할 경우에는 명명된 인스턴스를 사용합니다. 한 서버에서 기본 인스턴스 한 개만 호스팅할 수 있습니다.  
  
-   [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 를 설치하는 응용 프로그램은 이를 명명된 인스턴스로 설치해야 합니다. 이렇게 하면 여러 애플리케이션을 동일한 컴퓨터에 설치한 경우 충돌을 최소화할 수 있습니다.  
  
 **기본 인스턴스**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스를 설치하려면 이 옵션을 선택합니다. 한 컴퓨터에서는 기본 인스턴스를 하나만 호스팅할 수 있으며 나머지 인스턴스는 모두 명명된 인스턴스여야 합니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 인스턴스가 설치되어 있으면 동일한 컴퓨터에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 인스턴스를 추가할 수 있습니다.  
  
 **명명된 인스턴스**  
 새 명명된 인스턴스를 만들려는 경우 이 옵션을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 지정할 때 다음에 주의합니다.  
  
-   인스턴스 이름은 대/소문자를 구분하지 않습니다.  
  
-   인스턴스 이름은 밑줄(_)로 시작하거나 끝낼 수 없습니다.  
  
-   인스턴스 이름에는 용어 "Default" 또는 다른 예약 키워드를 사용할 수 없습니다. 인스턴스 이름에 예약 키워드를 사용한 경우 설치 오류가 발생합니다. 자세한 내용은 [예약된 키워드&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)를 참조하세요.  
  
-   인스턴스 이름으로 MSSQLServer를 지정하면 기본 인스턴스가 만들어집니다.  
  
-   [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 는 항상 'PowerPivot'이라고 명명된 인스턴스로 설치됩니다. 이 기능 역할에는 다른 인스턴스 이름을 지정할 수 없습니다.  
  
-   인스턴스 이름은 16자로 제한됩니다.  
  
-   인스턴스 이름의 첫 글자는 문자여야 합니다. 허용되는 문자는 유니코드 표준 2.0에서 정의된 문자입니다. 여기에는 a - z, A - Z의 라틴어 문자와 기타 언어의 문자가 포함됩니다.  
  
-   이어지는 글자는 유니코드 표준 2.0에 정의된 문자, 기본 라틴어 또는 기타 국가별 스크립트에 정의된 숫자, 달러 기호($) 또는 밑줄(_)이 될 수 있습니다.  
  
-   공백이나 다른 특수 문자는 인스턴스 이름에 사용할 수 없습니다. 백슬래시(\\), 쉼표(,), 콜론(:), 세미콜론(;), 작은따옴표('), 앰퍼샌드(&), 하이픈(-) 및 @ 기호도 사용할 수 없습니다.  
  
-   **사용할 수는 현재 Windows 코드 페이지에서 유효한 문자만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름입니다. 지원 되지 않는 유니코드 문자를 사용 하는 경우 설치 오류가 발생 합니다.**  
  
 **감지된 인스턴스 및 기능**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 실행 중인 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 구성 요소 목록을 확인합니다.  
  
 **인스턴스 ID** - 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 기본 인스턴스의 경우 인스턴스 이름 및 인스턴스 ID는 MSSQLSERVER입니다. 기본 인스턴스 ID가 아닌 ID를 사용하려면 **인스턴스 ID** 필드에 해당 ID를 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep을 사용할 경우 이 페이지에 표시되는 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 프로세스의 이미지 준비 단계 중에 지정한 인스턴스 ID입니다. 이미지 완료 단계에서는 다른 인스턴스 ID를 지정할 수 없습니다.  
  
> [!NOTE]  
>  밑줄(_)로 시작되거나 숫자 기호(#) 또는 달러 기호($)가 들어 있는 인스턴스 ID는 지원되지 않습니다.  
  
 디렉터리, 파일 위치 및 인스턴스 ID 명명에 대한 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하세요.  
  
 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 구성 요소는 하나의 단위로 관리됩니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩 및 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 구성 요소에 적용됩니다.  
  
 같은 인스턴스 이름을 공유하는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 다음 조건을 충족해야 합니다.  
  
-   **같은 버전**  
  
-   **같은 에디션**  
  
-   **같은 언어 설정**  
  
-   **같은 클러스터형 상태**  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 클러스터 인식형이 아닙니다.  
  
-   **같은 운영 체제**  
  
  
