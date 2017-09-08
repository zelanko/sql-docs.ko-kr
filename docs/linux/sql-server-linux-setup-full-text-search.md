---
title: "SQL Server 전체 텍스트 검색 linux 설치 | Microsoft Docs"
description: "이 항목에서는 Linux에서 SQL Server 전체 텍스트 검색을 설치 하는 방법에 설명 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.translationtype: MT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: a542817a861f968cebf3a66f91cfb016d2a685b8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/16/2017

---
# <a name="install-sql-server-full-text-search-on-linux"></a>Linux에서 SQL Server 전체 텍스트 검색 설치

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

다음 단계 설치 [SQL Server 전체 텍스트 검색](https://msdn.microsoft.com/library/ms142571.aspx) (**mssql-서버-fts**) linux. 전체 텍스트 검색을 사용 하면 SQL Server 테이블의 문자 기반 데이터에 대 한 전체 텍스트 쿼리를 실행할 수 있습니다. 이 릴리스의 알려진된 문제에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md)합니다.

> [!NOTE]
> 먼저 SQL Server 전체 텍스트 검색을 설치 하기 전에 [SQL Server 설치](sql-server-linux-setup.md#platforms)합니다. 이 구성 요소의 키 및 설치할 때 사용 하는 저장소는 **mssql-서버-fts** 패키지 합니다.

플랫폼에 대 한 SQL Server 전체 텍스트 검색을 설치 합니다.

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">RHEL에 설치</a>

다음 명령을 사용 하 여 설치는 **mssql-서버-fts** Red Hat Enterprise Linux에 있습니다. 

```bash
sudo yum update
sudo yum install -y mssql-server-fts
```

이미 있는 경우 **mssql-서버-fts** 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

오프 라인 설치 해야 할 경우에 전체 텍스트 검색 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 항목에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

## <a name="ubuntu">Ubuntu 설치</a>

다음 명령을 사용 하 여 설치 된 **mssql-서버-fts** ubuntu 합니다. 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

이미 있는 경우 **mssql-서버-fts** 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

오프 라인 설치 해야 할 경우에 전체 텍스트 검색 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 항목에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

## <a name="SLES">SLES에 설치</a>

다음 명령을 사용 하 여 설치는 **mssql-서버-fts** SUSE Linux Enterprise Server에 있습니다. 

```bash
sudo zypper install mssql-server-fts
```

이미 있는 경우 **mssql-서버-fts** 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

오프 라인 설치 해야 할 경우에 전체 텍스트 검색 패키지 다운로드를 찾습니다는 [릴리스 정보](sql-server-linux-release-notes.md)합니다. 다음 항목에 설명 된 동일한 오프 라인 설치 단계를 사용 하 여 [SQL Server 설치](sql-server-linux-setup.md#offline)합니다.

## <a name="supported-languages"></a>지원되는 언어

전체 텍스트 검색을 사용 하 여 [단어 분리기](https://msdn.microsoft.com/library/ms142509.aspx) 언어에 따라 개별 단어를 식별 하는 방법을 결정 하는 합니다. 쿼리를 통해 등록 된 단어 분리기의 목록을 가져올 수 있습니다는 **sys.fulltext_languages** 카탈로그 뷰에 있습니다. 다음 언어에 대 한 단어 분리기는 SQL Server 2017 RC2와 함께 설치 됩니다.

| 언어 | 언어 ID |
|---|---|
| 중립 | 0 |
| 아랍어 | 1025 |
| 벵골어(인도) | 1093 |
| 복말 | 1044 |
| 브라질어 | 1046 |
| 영어(영국) | 2057 |
| 불가리아어 | 1026 |
| 카탈로니아어 | 1027 |
| 중국어(홍콩 특별 행정구, 중국) | 3076 |
| 중국어(마카오 특별 행정구) | 5124 |
| 중국어(싱가포르) | 4100 |
| 크로아티아어 | 1050 |
| 체코어 | 1029 |
| 덴마크어 | 1030 |
| 네덜란드어 | 1043 |
| 영어 | 1033 |
| 프랑스어 | 1036 |
| 독일어 | 1031 |
| 그리스어 | 1032 |
| 구자라트어 | 1095 |
| Hebrew | 1037 |
| 힌디어 | 1081 |
| 아이슬란드어 | 1039 |
| 인도네시아어 | 1057 |
| 이탈리아어 | 1040 |
| 일본어 | 1041 |
| 카나다어 | 1099 |
| 한국어 | 1042 |
| 라트비아어 | 1062 |
| 리투아니아어 | 1063 |
| 말레이어 - 말레이시아 | 1086 |
| 말라얄람어 | 1100 |
| 마라티어 | 1102 |
| 폴란드어 | 1045 |
| 포르투갈어 | 2070 |
| 펀잡어 | 1094 |
| 루마니아어 | 1048 |
| 러시아어 | 1049 |
| 세르비아어(키릴 자모) | 3098 |
| 세르비아어(라틴 문자) | 2074 |
| 중국어(간체) | 2052 |
| 슬로바키아어 | 1051 |
| 슬로베니아어 | 1060 |
| 스페인어 | 3082 |
| 스웨덴어 | 1053 |
| 타밀어 | 1097 |
| 텔루구어 | 1098 |
| 태국어 | 1054 |
| 중국어(번체) | 1028 |
| 터키어 | 1055 |
| 우크라이나어 | 1058 |
| 우르두어 | 1056 |
| 베트남어 | 1066 |

## <a id="filters"></a>필터

전체 텍스트 검색 이진 파일에 저장 된 텍스트 에서도 작동 합니다. 하지만 경우 설치 된 필터는 파일을 처리 해야 합니다. 필터에 대 한 자세한 내용은 참조 [필터 구성 및 관리 검색에 대 한](https://msdn.microsoft.com/library/ms142499.aspx)합니다.

호출 하 여 설치 된 필터의 목록을 볼 수 **sp_help_fulltext_system_components 'filter'**합니다. SQL Server 2017 rc2 다음 필터 설치 됩니다.

| 구성 요소 이름 | 클래스 ID | 버전 |
|---|---|---|
|.a | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ans | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.asc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ascx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asm | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.asp | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.aspx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asx | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bas | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bat | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.bcp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.c | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cls | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cmd | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.csa | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.css | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.csv | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dbs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.def | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dic | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dos | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.dsp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.dsw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ext | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.faq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.fky | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.h | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hhc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hta | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.html | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htt | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htw | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.i | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ibq | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ics | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.idl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.idq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.inc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ini | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.inx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.jav | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.java | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.js | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.kci | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.lgn | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.log | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.m3u | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.mak | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.mk | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.odh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgdef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgundef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.prc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rc2 | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.reg | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rgs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rtf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rul | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|인스턴스입니다. | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.scc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.shtm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.shtml | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.snippet | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sol | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sor | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.srf | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.stm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.tab | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tdl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tlh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tli | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.trg | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.txt | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.udf | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.udt | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.url | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.usr | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vbs | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.viw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixlangpack | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixmanifest | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vspscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vssscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wri | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wtx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.xml | 41B9BE05-B3AF-460C-BF0B-2CDD44A093B1 | 12.0.9735.0 |

## <a name="semantic-search"></a>의미 체계 검색
[의미 체계 검색](https://msdn.microsoft.com/library/gg492075.aspx) 추출 하 고 통계적으로 관련성이 인덱스의 전체 텍스트 검색 기능에 빌드 *키 구*합니다. 이렇게 하면 데이터베이스에는 문서 내에서 의미를 쿼리할 수 있습니다. 또한이 유사한 문서를 식별할 수 있습니다.

의미 체계 검색을 사용 하려면 먼저 다운로드 하 고 연결 된 [의미 체계 언어 통계 데이터베이스](https://msdn.microsoft.com/library/gg509085.aspx)합니다.

1. Windows 컴퓨터에서 [다운로드는 합니다. 의미 체계 언어 통계 데이터베이스에 대 한 MSI 파일](https://www.microsoft.com/download/details.aspx?id=54277)합니다.

    > [!NOTE]
    > 이 다운로드는 데이터베이스에 대 한 시간을 합니다. MSI 파일 때문에 Windows 컴퓨터를이 단계에 대해 필요 합니다.

2. 실행 된 합니다. MSI 파일에서 데이터베이스를 추출할 및 로그 파일입니다.

3. Linux SQL Server 컴퓨터에 데이터베이스 및 로그 파일을 이동 합니다.

    > [!TIP]
    > Linux를 Windows에서 파일을 이동 하는 방법에 대 한 지침을 참조 하십시오. [Linux로 파일을 전송](sql-server-linux-migrate-restore-database.md#scp)합니다.

4. 언어 통계 데이터베이스를 연결 하 여 Linux SQL Server 인스턴스에서 다음 TRANSACT-SQL 명령을 실행 합니다.

    ```tsql
    CREATE DATABASE semanticsdb  
            ON ( FILENAME = N'var/opt/mssql/data/semanticsdb.mdf' )  
            LOG ON ( FILENAME = N'var/opt/mssql/data/semanticsdb_log.ldf' )  
            FOR ATTACH;  
    GO  
    ```

5. 의미 체계 언어 통계 데이터베이스를 등록 하려면 다음 TRANSACT-SQL 명령을 실행 합니다.

    ```tsql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO  
    ```

## <a name="next-steps"></a>다음 단계

전체 텍스트 검색에 대 한 정보를 참조 하십시오. [SQL Server 전체 텍스트 검색](../relational-databases/search/full-text-search.md)합니다. 

