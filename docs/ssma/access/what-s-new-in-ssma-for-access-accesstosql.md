---
title: Access 용 SSMA의 새로운 기능 (AccessToSQL) | Microsoft Docs
description: 각 릴리스에 대 한 AccessToSQL (액세스)에 대 한 변경 SQL Server Migration Assistant 내용에 대해 알아봅니다.
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 9/28/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: alexiva
ms.openlocfilehash: 5aaa4ad6a29d9582a8c62a94fbb94c18f79bfcff
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91497917"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Access 용 SSMA의 새로운 기능 (AccessToSQL)

이 문서에서는 각 릴리스의 액세스 변경에 대 한 SSMA (SQL Server Migration Assistant)를 나열 합니다.

## <a name="ssma-v814"></a>SSMA v 8.14

장애가 있는 사용자에 게 더 많은 접근성을 보장 하기 위해 몇 가지 개선 사항 외에도, Access 용 SSMA의 v 8.14 릴리스에는 이제 프로젝트를 업그레이드 해야 합니다. 이제 프로젝트 메타 데이터에 전체 원본/대상 서버 버전이 저장 됩니다.

## <a name="ssma-v813"></a>SSMA v 8.13

Access 용 SSMA의 v 8.13 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* `ORDER BY`절을 사용 하 여 변환 수정 `UNION`
* 필터링 된 고유 인덱스 지원
* 프로시저 및 함수 호출을 변환할 때 암시적 형식 캐스팅 고려

## <a name="ssma-v812"></a>SSMA v 8.12

Access 용 SSMA의 v 8.12 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* `BigInt`( `Large Number` ) 데이터 형식에 대 한 지원
* 향상 된 열 형식 확인
* 열 유효성 검사 규칙의 변환 향상
* 데이터 마이그레이션을 위해 사용 가능한 최신 ACE OLE DB 공급자 사용

## <a name="ssma-v811"></a>SSMA v 8.11

Access 용 SSMA의 v 8.11 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 대화형 Azure Active Directory 인증에 MSAL.NET 라이브러리 사용

## <a name="ssma-v810"></a>SSMA v 8.10

Access 용 SSMA의 v 8.10 릴리스에는 약간의 성능 향상 및 버그 수정이 포함 되어 있습니다.

## <a name="ssma-v89"></a>SSMA v 8.9

Access 용 SSMA의 v 8.9 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 자체 참조 쿼리를 위한 변환 향상
* 프로젝트 이름에서 특수 문자를 사용 하 여 문제 해결

## <a name="ssma-v88"></a>SSMA v 8.8

Access 용 SSMA의 v 8.8 릴리스에는 다음이 포함 됩니다.

* SQL Server 개체 동기화 안정성 향상
* 평가 및 변환 중 GUI 성능 향상
* 새 액세스 구문 파서를 사용 하 여 변환 성능 향상

## <a name="ssma-v87"></a>SSMA v 8.7

Access 용 SSMA의 v2.0 릴리스는 쿼리 기능에 대 한 변환 `IIF` 뿐만 아니라 그래픽 사용자 인터페이스의 사소한 수정 및 성능 향상 기능을 향상 시켰습니다.

> [!IMPORTANT]
> SSMA v 8.5 이상에서 .NET 4.7.2는 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v86"></a>SSMA v 8.6

사용자가 변환 된 코드에서 SSMA 확장 속성을 생략할 수 있도록 하는 설정을 추가 하 여, 유용성 및 성능을 향상 시키기 위해 설계 된 대상 수정 집합 외에도 Access 용 SSMA의 v 8.6 릴리스가 향상 되었습니다.

이 설정을 활용 하려면 Access 용 ssma에서 **도구**  >  **프로젝트 설정**  >  **일반**  >  **변환**으로 이동한 다음 **기타**에서 **확장 속성 생략** 설정의 값을 **예**로 업데이트 합니다.

![확장 속성 설정 생략](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> SSMA v 8.5 이상에서 .NET 4.7.2는 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v85"></a>SSMA v 8.5

Access 용 SSMA의 v 8.5 릴리스는 유용성 및 성능을 향상 시 키도 록 설계 된 대상 수정 집합과 함께 SQL server의 JSON 기능에 대 한 기본 지원 및 Azure Active Directory 인증을 지원 하 여 향상 되었습니다.

또한 Access 용 SSMA는 이제 여러 표준 함수 (, 등)의 변환을 지원 합니다. `ISNULL` `IIF`

> [!IMPORTANT]
> SSMA v 8.5를 사용 하는 경우 .NET 4.7.2 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v84"></a>SSMA v 8.4

Access 용 SSMA의 v 8.4 릴리스는 SQL Server 2016 이상 버전에 대 한 액세스 가능성 문제를 해결 하 고 max index 열 (16 대신 32을 허용 하도록)과 관련 된 버그를 수정 하기 위해 설계 된 대상 수정 기능을 사용 하 여 향상 되었습니다.

> [!IMPORTANT]
> SSMA 버전 7.4 (8.4)을 사용 하 여 .NET 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v83"></a>SSMA v 8.3

Access 용 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다. 또한 액세스에 대 한이 SSMA 릴리스는 다음을 수정 합니다.

* 접근성 문제를 해결 합니다.
* SQL Server 형식에 대 한 기본 지원을 추가 `hierarchyid` 합니다.

## <a name="ssma-v82"></a>SSMA v 8.2

액세스용 SSMA 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.1에서 v 8.2로 업데이트 하지 못할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v81"></a>SSMA v 8.1

액세스를 위한 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 대상 수정 기능으로 향상 되었습니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.0에서 v 8.1로의 업데이트가 실패할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v80"></a>SSMA v 8.0

Access 용 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 대상 수정 기능으로 향상 되었습니다. 또한이 릴리스는 다음과 같은 새로운 기능을 제공 합니다.

* 대상으로 **AZURE SQL Managed Instance** 지원. 이제 Azure SQL Managed Instance를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

* 변환 후 **수정 관리자**입니다. [여기](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733)에서 자세히 알아보세요.

* 예비 데이터베이스/스키마 선택.

    원본에 연결할 때 사용자는 이제 원하는 데이터베이스/스키마를 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택 하면 초기 연결 중에 시간이 절약 되 고 전체 SSMA 성능이 향상 됩니다.

   ![SSMA 필터 개체](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

Access 용 SSMA의 v 7.10 릴리스는 글로벌 요구 사항에 대 한 추가 보안 및 개인 정보 보호를 제공 하도록 설계 된 대상 수정 기능을 통해 향상 되었습니다.

## <a name="ssma-v79"></a>SSMA v 7.9

Access 용 SSMA의 v 7.9 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상 수정
* SSMA 명령줄에서 데이터 형식 매핑 및 프로젝트 기본 설정을 변경 하는 기능을 지원 합니다.
* 또한 SSMA의 Azure SQL Database 연결 대화 상자가 정규화 된 서버 이름을 지정 하도록 변경 되었습니다. 이전 버전의 SSMA에서는 Azure SQL Database 접두사가 프로젝트 설정 내에서 명시적으로 언급 되어야 했습니다.

## <a name="ssma-v78"></a>SSMA v 7.8

Access 용 SSMA의 v 7.8 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 프로젝트 설정에서 강조 표시 된 형식 매핑을 변경 합니다.
* 사용자가 원격 분석을 사용 하지 않도록 설정할 수 있는 기능입니다.

## <a name="ssma-v77"></a>SSMA v 7.7

Access 용 SSMA의 v 7.7 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상 수정
* 인기 있는 수요에 따라 액세스용 SSMA 32 비트 버전이 다시 사용 됩니다. 이전 구현에 비해 (v 7.4 이전)에는 두 개의 설치 관리자 패키지가 있지만 함께 설치할 수는 없습니다. 따라서 사용 중인 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 가능 하면 항상 64 비트 버전을 사용 하는 것이 좋습니다.

## <a name="ssma-v76"></a>SSMA v 7.6

Access 용 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 개선 하 고 SQL Server 2017 (공개 미리 보기)에 대 한 지원을 제공 하는 대상 수정 기능으로 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원은 공개 미리 보기 상태 이며 프로덕션 마이그레이션에 사용할 수 없습니다.

## <a name="ssma-v75"></a>SSMA v 7.5

장애가 있는 사용자에 게 더 많은 접근성을 보장 하기 위해 몇 가지 향상 된 기능으로 Access 용 SSMA의 v2.0 릴리스가 개선 되었습니다.

## <a name="ssma-v74"></a>SSMA v 7.4

Access 용 SSMA의 v 7.4 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 원본 및 대상에서 스키마 개체를 검색 하는 동안 **쿼리 제한 시간** 옵션을 사용할 수 있습니다.

  ![쿼리 제한 시간 옵션](../media/query-timeout_red.png)

* 사용자 의견에 따라 대상 수정으로 품질 및 변환 메트릭이 개선 되었습니다.

  > [!IMPORTANT]
  > .NET 4.5.2은 SSMA v 7.4를 설치 하기 위한 필수 구성 요소입니다. 또한 v 7.4부터 SSMA의 32 비트 버전이 더 이상 사용 되지 않습니다.

## <a name="ssma-v73"></a>SSMA v 7.3

Access 용 SSMA의 v 7.3 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 고객 의견을 기반으로 하는 대상 픽스로 품질 및 변환 메트릭이 개선 되었습니다.
* SSMA 확장성 프레임 워크는 다음 항목을 통해 노출 됩니다.
  * SQL Server Data Tools (SSDT) 프로젝트로 기능을 내보냅니다.
    * 이제 SSMA에서 SSDT 프로젝트로 스키마 스크립트를 내보낼 수 있습니다. 스키마 스크립트를 사용 하 여 추가 스키마 변경을 수행 하 고 데이터베이스를 배포할 수 있습니다.

        ![SSDT 프로젝트로 저장 명령](../media/export-schema-scripts_red.png)
  * 사용자 지정 변환을 수행 하기 위해 SSMA에서 사용할 수 있는 라이브러리입니다.
    * 이제 SSMA에서 이전에 처리 되지 않은 사용자 지정 구문 변환과 변환을 처리할 수 있는 코드를 생성할 수 있습니다.
      * 변환을 위한 샘플 프로젝트와 함께 사용자 지정 변환기를 구성 하는 방법에 대 한 지침은 [SQL Server Migration Assistant의 변환 기능을 확장](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181)하는 블로그 게시물에서 확인할 수 있습니다.

## <a name="ssma-v72"></a>SSMA v 7.2

Access 용 SSMA의 v 7.2 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 고객 의견을 기반으로 하는 대상 픽스로 품질 및 변환 메트릭이 개선 되었습니다.
* 향상 된 원격 분석을 통해 고객 문제를 해결 하 고 SSMA의 변환 속도를 개선할 수 있는 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v 7.1

Access 용 SSMA의 v 7.1 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 Windows 및 Linux CTP1의 SQL Server 2017는 마이그레이션에 지원 되는 대상 플랫폼입니다. 이 기능은 technical preview에 있으며 SQL server를 대상으로 하는 스키마 및 데이터 이동을 지원 합니다.
* 이제 SSMA가 자동 업데이트를 지원 하 여 최신 버전의 SSMA를 사용할 수 있는 즉시 다운로드 합니다.
* 이제 Windows Installer 패키지 파일 (.msi)을 통해 SSMA를 설치할 수 있는 이진 파일이 제공 됩니다.

## <a name="may-2016"></a>2016년 5월

Access 용 SSMA의 2016 년 5 월 릴리스는 다음과 같은 변경 내용을 포함 합니다.

* SQL Server 2016에 대 한 공식적인 지원이 추가 되었습니다.
* .NET 2.0에 대 한 설치 관리자 검사가 제거 되었습니다.
* `save-project` `open-project` Ssma 콘솔에 대 한 및 명령이 수정 되었습니다.
* `securepassword`SSMA 콘솔에 대 한 고정 명령입니다.
* 초기 로드에 대 한 개체 계산을 수정 했습니다.
* 액세스를 위한 UI 탭의 고정 테이블 데이터 로드
* 전역 설정에서 버그가 수정 되었습니다.

## <a name="march-2016"></a>2016년 3월

Access 용 SSMA의 2016 년 3 월 preview 릴리스는 SQL Server 2016로 마이그레이션에 대 한 지원을 추가 합니다.

## <a name="january-2016"></a>2016년 1월

Access 용 SSMA의 1 월 2016 유지 관리 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* GUID 필드의 기본값에 대 한 잘못 된 함수를 수정 했습니다 (RFC 3894811).
* SQL Database (Azure)로 레코드를 가져올 때 시스템이 응답을 중지 하는 문제를 해결 했습니다 (RFC 4919573).
* SSMA에 보기 로그 메뉴 항목을 추가 했습니다 (RFC 5706203).
* 원격 분석 추가.

## <a name="july-2014"></a>2014 년 7 월

Access 용 SSMA의 7 월 2014 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* Azure SQL Database 코드 변환을 개선 했습니다.
* Azure SQL Database를 지원 하기 위해 확장 팩 기능을 스키마로 이동 했습니다.
* 10k가 넘는 개체가 포함 된 데이터베이스에 대 한 성능 향상을 테스트 했습니다.
* 많은 수의 개체를 처리 하기 위한 UI 개선 기능이 추가 되었습니다.
* "잘 알려진" LOB 스키마를 강조 표시 하는 기능이 추가 되었습니다. 변환 시 무시 될 수 있습니다.
* 변환 속도 개선 기능이 추가 되었습니다.
* UI의 개체 수를 표시 하기 위한 지원이 추가 되었습니다.
* 20%를 초과 하 여 보고서 크기를 줄였습니다.
* 구문 분석 되지 않은 구문에 대 한 오류 메시지가 개선 되었습니다.

## <a name="april-2014"></a>2014년 4월

Access 용 SSMA의 4 월 2014 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* MS SQL Server 2014에 대 한 지원이 추가 되었습니다.
* Azure로의 변환과 관련 된 버그가 수정 되었습니다.
* IE 10의 보이지 않는 보고서 페이지와 관련 된 버그가 수정 되었습니다.

## <a name="january-2012"></a>2012년 1월

Access 용 SSMA의 1 월 2012 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 마이그레이션 후 MS Access 연결 된 테이블에 대 한 사용자 이름 및 암호를 유지 하지 않는 옵션을 제공 했습니다.
* 순환 참조에 대 한 cascade 동작을 No Action으로 설정 합니다.
* 순환 참조에 대 한 cascade 동작을 나타내는 적절 한 메시지를 작업 없음으로 설정 했습니다.

## <a name="july-2011"></a>2011년 7월

Access 용 SSMA의 7 월 2011 릴리스는 데이터 마이그레이션 중에 향상 된 오류 보고 기능을 추가 합니다.

## <a name="april-2011"></a>4 월 2011

Access 용 SSMA의 4 월 2011 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] 및 Azure SQL을 지 원하는 "ssma for Access"가 설치 된 단일를 추가 했습니다 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* 에 연결 하는 기능이 추가 되었습니다 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* 이전 버전과의 호환성을 위해 Access Console 용 SSMA 버전 지원을 추가 했습니다. 이전 버전에서 만든 프로젝트를 SSMA v 5.0으로 열 수 있습니다.
* 이전 버전의 SSMA 제품에서 SxS ()를 설치 하는 기능이 추가 되었습니다.

## <a name="july-2010"></a>2010년 7월

Access 용 SSMA의 7 월 2010 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* SQL Server 2008 R2 및 Azure SQL로 마이그레이션에 대 한 지원이 추가 되었습니다.
* SQL Server 및 Azure SQL에 대 한 보안 연결을 추가 했습니다.
* Access 2010 데이터베이스에 대 한 지원이 추가 되었습니다.
* 명령줄 실행을 위한 새 SSMA 콘솔 응용 프로그램이 추가 되었습니다.
* SQL Server 데이터 형식에 대 한 지원이 추가 되었습니다 `DateTime2` .

## <a name="june-2008"></a>6 월 2008

Access 용 SSMA의 6 월 2008 릴리스는 Access 2007 데이터베이스에 대 한 지원을 추가 합니다.

## <a name="may-2007"></a>2007 년 5 월

Access 용 SSMA의 2007 년 5 월 릴리스는 다음과 같은 변경 내용을 포함 합니다.

* 작업 그룹 정책을 사용 하는 Access 데이터베이스에 대 한 지원이 추가 되었습니다.
* SQL Server 메타 데이터 탐색기에서 변환 된 개체를 삭제 하는 기능을 제공 합니다.
* SQL Server 형식의 SQL 모드에서 사용자가 입력 한 주석에 대 한 지원이 추가 되었습니다.
* 개체 변환 기능이 향상 되었습니다.

## <a name="november-2006"></a>11 월 2006

Access 용 SSMA의 11 월 2006 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 단일 데이터베이스를로 마이그레이션하는 과정을 안내 하는 새 데이터베이스 마이그레이션 마법사가 추가 되었습니다 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] .
* Access 데이터베이스를 변환 하 고, 변환 된 개체를에 로드 하 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 고, 데이터를 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 모두 한 번에 마이그레이션하는 새 변환, 로드 및 마이그레이션 명령을 추가 했습니다.
* 향상 된 쿼리 마이그레이션. 이제 쿼리 마이그레이션이 더 많은 SELECT 쿼리를 뷰로 변환 합니다. 자세한 내용은 [Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)을 참조 하세요.
* 테이블 탭의 테이블 및 인덱스 속성을 편집 하는 기능이 추가 되었습니다 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] **Table** .
* 새 전역 설정이 추가 됨:
  * 편집기 창에 줄 번호를 표시 하도록 선택할 수 있습니다.
  * 중복 된 개체를 바꿀지 묻는 메시지를 표시 하도록 SSMA를 구성 하거나 스키마를 변환 하는 동안 중복 개체를 항상 또는 절대 바꾸지 않도록 구성할 수 있습니다.
* 복합 쿼리에 와일드 카드가 포함 된 경우 SSMA에서 경고를 표시할지 여부를 지정할 수 있는 새로운 변환 옵션이 추가 되었습니다.

## <a name="july-2006"></a>7 월 2006

Access 용 SSMA의 7 월 2006 릴리스는 초기 릴리스입니다.
