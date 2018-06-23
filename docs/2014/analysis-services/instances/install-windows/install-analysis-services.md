---
title: 테이블 형식 모드에서 Analysis Services 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f6fabd9129e3f3e1e07e813935f36e7c70c48072
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092982"
---
# <a name="install-analysis-services-in-tabular-mode"></a>테이블 형식 모드에서 Analysis Services 설치
  새로운 테이블 형식 모델링 기능을 사용하기 위해 Analysis Services를 설치하는 경우 모델 유형을 지원하는 서버 모드에서 Analysis Services를 설치해야 합니다. 서버 모드는 테이블 형식이고 설치 동안 구성됩니다.  
  
 이 모드로 서버를 설치한 이후에 테이블 형식 모델 디자이너에서 작성하는 호스트 솔루션을 사용할 수 있습니다. 네트워크를 통해 테이블 형식 모델 데이터에 액세스하려는 경우 테이블 형식 모드 서버가 필요합니다.  
  
 설치 마법사에서 또는 명령줄 설치에서 테이블 형식 모드를 지정할 수 있습니다. 다음 섹션에서는 각 방법에 대해 설명합니다.  
  
## <a name="installation-wizard"></a>설치 마법사  
 다음 목록에서는 테이블 형식 모드의 Analysis Services를 설치하는 데 사용되는 SQL Server 설치 마법사의 해당 페이지를 보여 줍니다.  
  
1.  설치 프로그램의 기능 트리에서 **Analysis Services** 를 선택합니다.  
  
     ![Analsyis 서비스를 보여 주는 설치 기능 트리에](../../../sql-server/install/media/ssas-setupas.gif "Analsyis 서비스를 보여 주는 설치 기능 트리에")  
  
2.  Analysis Services 구성 페이지에서 **테이블 형식 모드**를 선택해야 합니다.  
  
     ![Analysis Services 구성 옵션으로 설치 페이지](../../../sql-server/install/media/ssas-setupasconfig.gif "Analysis Services 구성 옵션으로 설치 페이지")  
  
 테이블 형식 모드는 xVelocity 메모리 내 분석 엔진(VertiPaq)을 사용합니다. 이 엔진은 Analysis Services에 배포하는 테이블 형식 모델에 대한 기본 저장소입니다. 테이블 형식 모델 솔루션을 서버에 배포한 이후에 테이블 형식 솔루션을 선택적으로 구성하여 메모리 집중형 저장소 대신에 DirectQuery 디스크 저장소를 사용할 수 있습니다.  
  
## <a name="command-line-setup"></a>명령줄 설치  
 SQL Server 설치에는 서버 모드를 지정하는 새로운 매개 변수(`ASSERVERMODE`)가 포함됩니다. 다음 예에서는 테이블 형식 서버 모드에 Analysis Services를 설치하는 명령줄 설치를 보여 줍니다.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 `INSTANCENAME` 17 자 미만 이어야 합니다.  
  
 모든 자리 표시자 계정 값을 유효한 계정 및 암호로 바꾸어야 합니다.  
  
 SQL Server Management Studio 또는 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]와 같은 도구는 제공되는 명령줄 구문 예를 사용하여 설치되지 않습니다. 기능을 추가 하는 방법에 대 한 자세한 내용은 참조 [명령 프롬프트에서 SQL Server 2014 설치](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)합니다.  
  
 `ASSERVERMODE` 대/소문자 구분입니다.  모든 값은 대문자로 표시해야 합니다. 다음 표에는 `ASSERVERMODE`의 유효한 값에 대한 설명이 나와 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|이것은 기본값입니다. 설정 하지 않으면 `ASSERVERMODE`, 서버는 다차원 서버 모드에 설치 됩니다.|  
|POWERPIVOT|이 값은 선택 사항입니다. 실제로 `ROLE` 매개 변수를 설정한 경우 서버 모드는 자동으로 1로 설정되며 `ASSERVERMODE`를 SharePoint용 PowerPivot 설치에 대한 옵션으로 만듭니다. 자세한 내용은 참조 [명령 프롬프트에서 PowerPivot 설치](../../../sql-server/install/install-powerpivot-from-the-command-prompt.md)합니다.|  
|TABULAR|명령줄 설치를 사용하여 테이블 형식 모드에 Analysis Services를 설치하는 경우 이 값이 필요합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 인스턴스의 서버 모드 확인](../determine-the-server-mode-of-an-analysis-services-instance.md)   
 [메모리 내 또는 테이블 형식 모델 데이터베이스에 대 한 DirectQuery 액세스 구성](../../tabular-models/enable-directquery-mode-in-ssms.md)   
 [테이블 형식 모델링 &#40;SSAS 테이블 형식&#41;](../../tabular-models/tabular-models-ssas.md)  
  
  