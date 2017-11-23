---
title: "배포 하 고 분석 mrsdeploy를 사용 하 여 사용할 | Microsoft Docs"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0bd3095fbb41beeb5d31d8c64dc5969acfdb3c9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="deploy-and-consume-analytics-using-mrsdeploy"></a>배포 및 mrsdeploy를 사용 하 여 분석 사용

Microsoft R Server에는 해결해줍니다 기능이 **mrsdeploy**, 이러한 작업을 지 원하는:

+ 게시 및 R 및 Python 모델 및 웹 서비스의 형태로 코드를 관리 합니다.
+ 클라이언트 응용 프로그램 내에서 이러한 서비스를 사용합니다.

이 항목에서는 기능을 구성 하는 방법에 대 한 정보를 제공 합니다.

지 원하는 시나리오에 대 한 일반적인 내용은 **mrsdeploy**, 참조 [R server 해결해줍니다](https://docs.microsoft.com/r-server/what-is-operationalization)합니다.

## <a name="using-mrsdeploy-for-operationalization"></a>Mrsdeploy 화에 대 한 사용 하 여

단어 *해결해줍니다* 많은 것을 의미할 수 있습니다.

+ 응용 프로그램에서 사용 하기 위해 웹 서비스에 모델을 게시 하는 기능
+ Scalable 또는 분산 컴퓨팅에 대 한 지원
+ 한 번 개발, 여러 번 배포
+ 모두 단일 행에 대 한 빠른 점수 및 일괄 처리 점수 매기기

SQL Server와 함께 컴퓨터 학습 서비스를 설치한 경우 *해결해줍니다* 은 저장된 프로시저에서 R, Python 코드를 래핑하여의 문제입니다. 모든 응용 프로그램 모델을 다시 학습, 점수를 생성 또는 보고서를 만드는 저장된 프로시저를 호출할 수 있습니다. 또한 SQL Server의 기존 일정 예약 메커니즘을 사용 하 여 작업을 자동화할 수 있습니다.

그러나 Microsoft R Server는 배포 된 R 작업 실행을 위한 관리 유틸리티 및 R 작업의 게시를 지 원하는 웹 서비스를 사용 하 여 배포 지원에 대 한 다른 메커니즘을 제공 합니다. Microsoft R Server에 기능을 사용 하 여 **mrsdeploy** 패키지를 원격 계산 노드와 세션을 설정 하 고 콘솔 응용 프로그램에서 R 코드를 실행 합니다.

이 배포 기능은 R Server의 이러한 이점을 제공합니다.

+ 분석 웹 서비스에 역할 기반 액세스 제어

    게시, 업데이트 및 웹 서비스를 삭제할 수 있는 결정, 업데이트 및 웹 서비스를 삭제할 수도 사용자에 게 수 있는 유일한 목록 다른 사용자와 사용자가 게시 웹 서비스를 사용 합니다.

+ 더 빠르게 점수 매기기
  
  지원 되는 R 모델 개체와 점수 매기기 실시간 작업 점수 매기기의 속도 개선 하기 위해 사용할 수 있습니다.

+ Python 코드를 웹 서비스로 게시

  예제를 보려면 [게시 Python 코드 사용 및](./python/publish-consume-python-code.md)합니다.

+ 비동기 일괄 처리 사용

  일괄 처리 실행을 통해 큰 입력된 데이터에 대 한 호출 하는 웹 서비스를 비동기적으로 이제 사용할 수 있습니다.

+ 웹 및 계산 노드의 눈금의 자동 크기 조정

  스크립트 템플릿은 사용 하면 Azure에서 R 서버 Vm 집합을 쉽게 스핀업 하 고 분석 및 원격 실행 작업 활용에 대 한 표로 구성에 제공 됩니다. 이 표는 수직 확장 또는 CPU 사용량을 기준으로 아래로 수 있습니다.

+ 비동기 원격 실행

    지금 사용 하 여 지원 되는 **mrsdeploy** R 패키지 합니다. 비동기적으로 사용 하 여 R 스크립트 실행 개발 환경에서 원격 스크립트를 실행 하는 동안 작업을 계속 하려면는 `async` 매개 변수입니다. 실행 시간이 긴 스크립트를 실행 하는 경우 특히 유용 합니다.

## <a name="requirements-and-configuration"></a>요구 사항 및 구성

SQL Server 2017 CTP 2.0 이상에 R Server에만 사용할 수 있었던 되었고 SQL Server R services 설치 되어 있지 않습니다는이 기능이 포함 됩니다. **mrsdeploy** 설치 하는 옵션을 선택 하는 경우 패키지를 SQL Server 컴퓨터에 설치 되어 **Microsoft 컴퓨터 학습 서버**에서 **공유 기능** SQL Server 설치 프로그램의 섹션입니다.

일반적으로 SQL Server 컴퓨터 학습 서비스를 실행 하는 동일한 컴퓨터에 서버를 학습 하는 컴퓨터를 설치 하지 않는 것이 좋습니다. 설치 하는 것이 좋습니다 **Microsoft 컴퓨터 학습 서버** SQL Server에서 별도 컴퓨터에 한 다음 해당 컴퓨터에서 화 기능을 구성 합니다.

그러나 함께 설치 해야 할 경우 성공적으로 서비스를 구성 하려면 다음 추가 단계를 수행 합니다.

1. DotNetCore 1.1 설치

    .NET Core를 SQL Server의 일부로 설치 되지 않은 경우 R Server 설치 프로그램을 시작 하기 전에 설치 해야 합니다.

2. Microsoft 컴퓨터 학습 서버를 설치 합니다.

3. 설치를 마친 후 **Microsoft 컴퓨터 학습 서버**수동으로 다음 레지스트리 키에 대 한 추가 **mrsdeploy**, R_SERVER 파일에 대 한 기본 폴더를 지정 하는 합니다. 

    + 새 레지스트리 키 만들기`H_KEY_LOCAL_MACHINE\SOFTWARE\R Server\Path`
    + 키의 값을 설정 `"C:\Program Files\Microsoft SQL Server\140\R_SERVER"`합니다.

4. 을 완료 한 후 엽니다는 [관리자 유틸리티](https://docs.microsoft.com/r-server/operationalize/configure-use-admin-utility)합니다.

5. 계속 구성할는 **mrsdeploy** 여기에 설명 된 대로 서비스: [관리자를 위한 구성](https://docs.microsoft.com/r-server/operationalize/configure-start-for-administrators)

6. 자세한 내용은 참조 [mrsdeploy 함수](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)합니다.
