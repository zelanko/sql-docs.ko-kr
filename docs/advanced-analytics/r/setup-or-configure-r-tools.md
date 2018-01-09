---
title: "SQL Server 설치 프로그램에 포함 된 R 도구 | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b45c1a9c58ede0342953caae58c3bd6822501c24
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="r-tools-included-with-sql-server-setup"></a>SQL Server 설치 프로그램에 포함 된 R 도구

함께 설치 된 동일한 R 도구를 가져오는 R SQL Server를 설치 하면 **기본** 관리자 권한, rterm이, 등의 r을 설치 합니다. 따라서 기술적으로 개발 하 고 R 코드를 테스트 하는 데 필요한 모든 도구.

이 항목에서는 설치에 포함 된 도구를 나열 합니다.

> [!TIP]
> 
> 일반적으로 디버깅 하 고 전용된 개발 환경을 사용 하 여 R 코드를 테스트할 쉽습니다. 에서 테스트해 보는 것 미리 외부 도구를 자세한 오류 메시지를 읽을 하 고 솔루션을 디버그할 수 있도록 하는 경우 SQL Server에서 R 코드를 실행 하는 보다 쉽게 찾을 수 있습니다.
> 
> 이 문서를 목록에 대 한 SQL Server와 함께 작동 하도록 구성 하는 방법 및 R 솔루션을 개발 하는 데 사용할 수 있는 무료 도구 참조: [데이터 과학 클라이언트 설정](set-up-a-data-science-client.md)

**적용 대상:** SQL Server 2016 R Services (In-database) 및 Microsoft R Server (독립 실행형) SQL Server 2017 기계 학습 Services (In-database) 및 기계 학습 Server (독립 실행형)

## <a name="r-tools-included-with-installation"></a>설치에 포함 된 R 도구

에 포함 된 다음 표준 R 도구는 *설치 기본* r을 기본적으로 설치 되 고 있습니다.

+ **Rterm이**: R 스크립트를 실행 하기 위한 명령줄 터미널

+ **RGui.exe**: R에 대한 간단한 대화형 편집기입니다. RGui.exe 및 RTerm에 대한 명령줄 인수는 동일합니다.

+ **RScript**: 일괄 처리 모드에서 R 스크립트를 실행하기 위한 명령줄 도구입니다.

이러한 도구를 찾으려면 SQL Server 또는 독립 실행형 기계 학습 기능을 설정할 때 설치 된 R 라이브러리를 확인 합니다. 예를 들어 기본 설치의 경우 R 도구가 이러한 폴더에 있습니다.

+ SQL Server 2016 R Services:`~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server 독립 실행형:`~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 2017 컴퓨터 학습 서비스:`~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ 서버 (독립 실행형)를 학습 하는 컴퓨터:`~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

R 도구에서 도움이 필요한 경우 열기만 **관리자 권한**, 클릭 **도움말**, 고 옵션 중 하나를 선택 합니다.

## <a name="introducing-microsoft-r-client"></a>Microsoft R 클라이언트를 소개합니다.

Microsoft R 클라이언트는 개발 사용 하기 위해 RevoScaleR 패키지에 액세스할 수 있는 무료 다운로드 합니다. R 클라이언트를 설치 하 여 SQL Server 데이터베이스에 분석 및 분산 R 컴퓨팅 Hadoop, Spark, 또는 Linux 컴퓨터 학습 서버를 사용 하 여에 포함 하 여 모든 지원 되는 계산 컨텍스트에서 실행할 수 있는 R 솔루션을 만들 수 있습니다.

다른 R 개발 환경을 이미 설치한 경우 등 RStudio, 라이브러리 및 Microsoft R 클라이언트에서 제공 되는 실행 파일을 사용 하도록 환경을 다시 구성 해야 합니다. 이렇게 하면 RevoScaleR 패키지의 모든 기능을 사용할 수 있습니다 성능 제한 됩니다.

자세한 내용은 참조 [Microsoft R Client 란?](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)
