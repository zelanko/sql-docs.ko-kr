---
title: "R 도구 설치 또는 구성 | Microsoft 문서"
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3baf97a960d7e8f950bb6e9cd251550f4c4b942
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="setup-or-configure-r-tools"></a>R 도구 설치 또는 구성
  Microsoft R Server는 모든 기본 R 라이브러리, ScaleR 패키지 집합 및 R 코드를 개발 및 테스트하는 데 필요한 표준 R 도구를 제공합니다. 하지만 전용 R 개발 환경을 사용하려는 경우 다양한 무료 도구를 포함하여 여러 가지 도구를 사용할 수 있습니다.  
  
## <a name="basic-r-tools"></a>기본 R 도구  
 R의 *기본 설치*에 포함된 모든 표준 R 도구는 기본적으로 설치되므로 Microsoft R Server 설치 시에는 추가 도구가 필요하지 않습니다.

-   **RTerm**: R 스크립트를 실행하기 위한 명령줄 도구입니다. 
  
-   **RGui.exe**: R에 대한 간단한 대화형 편집기입니다. RGui.exe 및 RTerm에 대한 명령줄 인수는 동일합니다. 
  
-   **RScript**: 일괄 처리 모드에서 R 스크립트를 실행하기 위한 명령줄 도구입니다.  

이러한 도구를 찾으려면 R 라이브러리 위치를 찾아봅니다. 이 위치는 SQL Server R Services만 설치했는지, 아니면 R Server(독립 실행형)도 설치했는지에 따라 달라집니다. 자세한 내용은 [설치된 기능 및 R 패키지를 찾을 수 있는 위치](https://msdn.microsoft.com/library/mt695941(sql.130).aspx#Anchor_1)를 참조하세요.

그 다음에 `..\R_SERVER\bin\x64` 폴더를 찾아봅니다.  

> [!TIP]  
>  R 도구와 관련된 도움말이 필요하세요? 설명서는 설치 폴더 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` 및 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`에 있습니다.  
>   
>  또는 **RGui**를 열고 **도움말**을 선택하고 나서 옵션 중 하나를 선택합니다.  

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R Client는 Microsoft R Server 또는 SQL Server R Services에서 쉽게 실행할 수 있는 R 솔루션을 개발하는 데 사용되는 무료 다운로드입니다. 이 옵션은 R Server(Enterprise Edition에서 사용 가능)에 액세스할 수 없는 데이터 과학자가 ScaleR을 사용하는 솔루션을 개발하도록 지원하기 위해 제공됩니다. 

R Tools for Visual Studio 또는 RStudio와 같은 다른 R 개발 환경을 사용할 경우 ScaleR을 사용하려면 Microsoft R Client가 R 실행 파일로 사용되도록 지정해야 합니다. 이렇게 하면 성능이 제한되지만 RevoScaleR 패키지 및 Microsoft R Server의 기타 기능에 대한 전체 액세스 권한이 제공됩니다.

RGui 및 RTerm과 같이 R Client에 제공된 도구를 사용하여 스크립트를 실행하거나 임시 R 코드를 작성하고 실행할 수도 있습니다.

[Install Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install)(Microsoft R Client 설치)
  
##  <a name="bkmk_RTools"></a> R Tools for Visual Studio  

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 간편하게 사용할 수 있도록 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]를 개발 환경으로 사용하는 것이 좋습니다. [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]는 모든 Visual Studio 버전에서 작동하는 Visual Studio의 무료 추가 기능입니다. Visual Studio는 Python 및 F# 통합에 대한 지원도 제공합니다.  

 설치 지침을 참조 하십시오. [Visual Studio에 대 한 R 도구를 설치 하는 방법을](https://docs.microsoft.com/visualstudio/rtvs/installation)합니다.

> [!TIP]
> 새 패키지를 설치하기 전에 기본적으로 사용 중인 R 런타임을 확인합니다. 실행 중이 아니면 새 R 패키지를 기본 라이브러리 위치에 매우 쉽게 설치할 수 있고 R Server에서 찾지 않아도 됩니다.


## <a name="rstudio"></a>RStudio

RStudio를 사용하려면 RevoScaleR 라이브러리를 사용하기 위한 몇 가지 추가 단계가 필요합니다.
- Microsoft R Server 또는 Microsoft R Client를 설치하여 필요한 패키지와 라이브러리를 가져옵니다.
- R Server 런타임을 사용하도록 R 경로를 업데이트합니다.

자세한 내용은 [Configure Your IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)(IDE 구성)를 참조하세요.


## <a name="see-also"></a>참고 항목  
 [독립 실행형 R Server 만들기](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Microsoft R Server&#40;독립 실행형&#41; 시작](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  

