---
title: "Python 상호 운용성 | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32762183ff5273998848978238788cc830319b91
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="python-interoperability"></a>Python 상호 운용성

이 항목의 기능을 사용 하면 설치 된 Python 구성 요소를 설명 **컴퓨터 학습 Services (In-database)** Python를 언어로 선택 합니다.

> [!NOTE]
> Python에 대 한 지원 시험판 기능이 며 아직 개발 중인 합니다.

## <a name="python-components"></a>Python 구성 요소

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]Python 실행 파일을 수정 하지 않습니다. Python 런타임의 SQL 도구와 독립적으로 설치 되어 있고 외부에서 실행 되는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 프로세스입니다.

연결 된 특정 배포 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스는 인스턴스와 연결 된 폴더에서 찾을 수 있습니다.

예를 들어 기본 인스턴스는 Python 옵션으로 컴퓨터 학습 서비스를 설치 하는 경우 아래를 봅니다.

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER`

SQL Server 2017 컴퓨터 학습 서비스의 설치는 python Anaconda 배포를 추가합니다. 특히, Anaconda 4.3 분기에 따라 Anaconda 3 설치 관리자는 사용 합니다. SQL Server 2017에 대 한 예상된 Python 수준은 Python 3.5입니다.

## <a name="new-in-this-release"></a>이 릴리스의 새로운 기능

Continuum analytics 사이트 참조 목록이 Anaconda 배포에서 지 원하는 패키지에 대 한: [Anaconda 패키지 목록](https://docs.continuum.io/anaconda/pkg-docs)

SQL Server 2017에 컴퓨터 학습 서비스도 포함 되어 새 **revoscalepy** Python에 대 한 라이브러리입니다.

것과 동일한 기능을 제공 하는이 라이브러리는 **RevoScaleR** Microsoft r 패키지 즉, 지원으로 원격 계산 컨텍스트는 다양 한 확장 가능한 기계 학습 모델 만들기와 같은 **rxLinMod**합니다. RevoScaleR에 대 한 자세한 내용은 참조 [분산 및 병렬 컴퓨팅을 ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)합니다.

때문에 Python는 시험판 기능 및 개발 중인 여전히 지원는 **revoscalepy** 라이브러리에는 현재 RevoScaleR 기능의 하위 집합만 포함 됩니다. 

앞으로 추가 될 포함 될 수 있습니다는 [Microsoft Cognitive Toolkit](https://www.microsoft.com/research/product/cognitive-toolkit/)합니다. 이 라이브러리 이전의 CNTK, 다양 한 convolutional 네트워크 (만우절), 되풀이 네트워크 (같은 메시지가) 및 짧은 용어 메모리 긴 네트워크 (LSTM)를 포함 하 여 신경망 모델을 지원 합니다.

## <a name="using-python-in-sql-server"></a>SQL Server에서 Python 사용

가져올는 **revoscalepy** 변환한 다음 프로그램 Python 코드 모듈에서 함수를 호출 하는 모듈 같은 다른 모든 Python 함수입니다.

Python에 대 한 입력된 데이터를 테이블 형식 이어야 합니다. 모든 Python 결과의 형태로 반환 되어야 합니다는 **팬더** 데이터 프레임입니다.

저장된 프로시저에서 스크립트를 포함 하 여 T-SQL, 내부 Python 코드를 실행할 수 있습니다.

또는 코드를 실행 하는 로컬 인 Python IDE에서 있고 원격 계산 컨텍스트를 정의 하 여 SQL Server 컴퓨터에서 실행 되는 스크립트.

로컬 데이터를 사용 하거나 SQL Server 또는 기타 ODBC 데이터 원본에서 데이터를 가져올 XDF 파일 형식을 사용 하 여 R 솔루션 또는 다른 소스와 데이터를 교환할 수 있습니다.

**자세한 내용은**

+ 지원 되는 함수: [revoscalepy 란](what-is-revoscalepy.md) 
+ 지원 되는 Python 데이터 형식: [Python 라이브러리 및 데이터 형식](python-libraries-and-data-types.md)
+ 지원 되는 데이터 소스: ODBC 데이터베이스, SQL Server 및 XDF 파일
+ 계산 컨텍스트를 지원: 로컬 또는 SQL Server

### <a name="licensing"></a>라이선스

Python 컴퓨터 학습 서비스의 설치 과정의 일부로 GNU Public License 약관에 동의 해야 합니다.

## <a name="see-also"></a>관련 항목:

[Python 라이브러리 및 데이터 형식](python-libraries-and-data-types.md)

