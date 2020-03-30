---
title: 데이터베이스 프로젝트로 가져오기
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLPROJECTIMPORTSNAPSHOTSUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.SQLPROJECTIMPORTDATABASESUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.IMPORTSCRIPTWIZARD.SUMMARY
ms.assetid: d0a0a394-6cb6-416a-a25f-9babf8ba294a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 0cfdbb9cb094188e372424257656953b62635996
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246448"
---
# <a name="import-into-a-database-project"></a>데이터베이스 프로젝트로 가져오기

가져오기를 사용하여 라이브 데이터베이스 또는 .dacpac의 새 개체로 프로젝트를 채우거나 프로젝트의 기존 개체를 스크립트의 새 정의로 업데이트할 수 있습니다. 이러한 세 경로 사이에는 아래 설명과 같이 주목할 몇 가지 동작 차이가 있습니다.  
  
**가져오기 메뉴**  
  
![SSDT 가져오기 메뉴](../ssdt/media/ssdt-import.gif "SSDT 가져오기 메뉴")  
  
**이 항목의 단원**  
  
[가져오기 원본: 데이터베이스 또는 데이터 계층 애플리케이션(*.dacpac)](#bkmk_import_source_db)  
  
[가져오기 원본: 스크립트(*.sql)](#bkmk_import_source_script)  
  
[암호화된 개체 가져오기](#bkmk_import_encrypted)  
  
## <a name="import-source-database-or-data-tier-application-dacpac"></a><a name="bkmk_import_source_db"></a>가져오기 원본: 데이터베이스 또는 데이터 계층 애플리케이션(*.dacpac)  
데이터베이스 또는 .dacpac 파일에서 스키마를 가져오는 기능은 프로젝트에 정의된 스키마 개체가 없을 경우에만 사용할 수 있습니다. 여기에는 RefactorLog 또는 배포 전/배포 후 스크립트가 포함되지 않습니다.  
  
가져올 때에는 새 개체에 대한 SSDT의 조직적 기본값을 사용하여 개체 정의가 프로젝트 파일에 스크립트로 작성됩니다. 최상위 개체에 대한 새 파일, 동일한 파일에 같은 부모로 정의된 계층적 자식, 가능할 경우 인라인으로 정의된 테이블/열 제약 조건. 각 개체에 대해 더 구체적인 표시 유형과 제어를 사용하려면 가져오기 대신 스키마 비교를 사용하십시오.  
  
가져오기 원본에 배포 전 및 배포 후 스크립트, RefactorLog 또는 SQLCMD 변수 정의가 포함되어 있는 경우 프로젝트로 가져올 수 있습니다. 프로젝트에 이러한 아티팩트 중 하나라도 이미 포함되어 있을 경우 가져온 파일은 프로젝트의 **가져오기 시 무시됨** 폴더에 추가됩니다.  
  
**가져오기 시 무시됨 폴더**  
  
![SSDT 가져오기 시 무시됨 폴더](../ssdt/media/ssdt-ignoredonimport.gif "SSDT 가져오기 시 무시됨 폴더")  
  
## <a name="import-source-script-sql"></a><a name="bkmk_import_source_script"></a>가져오기 원본: 스크립트(*.sql)  
프로젝트에 ‘없었던’ 가져오기 원본의 모든 개체가 추가되며, 프로젝트에 ‘이미 있었던’ 가져오기 원본의 모든 개체는 프로젝트의 개체 정의를 덮어씁니다.    
  
> [!NOTE]  
> 이 경로에는 향후 릴리스에서 수정될 두 가지 알려진 버그가 있습니다.  
>   
> -   프로젝트의 테이블 정의에서 테이블/열 제약 조건이 CREATE TABLE 문 밖에서 정의된 경우 가져오기가 테이블 정의를 덮어써서 제약 조건이 인라인이 됩니다. 하지만 인라인이 아닌 제약 조건은 그대로 두기 때문에 프로젝트에 중복되는 제약 조건이 생깁니다.  
> -   가져오기 작업 시 프로젝트에 이미 존재했던 원본 스크립트의 마스터 키 또는 데이터베이스 암호화 키는 중복됩니다. 프로젝트를 빌드할 수 있도록 중복을 제거하십시오.  
  
스크립트에서 가져오기 프로세스는 배포 전/배포 후 스크립트, SQLCMD 변수 또는 RefactorLog 파일을 이해하지 못합니다. 이러한 항목과 가져올 때 감지된 지원되지 않는 구문은 프로젝트에서 **스크립트** 폴더의 **ScriptsIgnoredOnImport.sql** 파일에 배치됩니다.  
  
 
## <a name="import-encrypted-objects"></a><a name="bkmk_import_encrypted"></a>암호화된 개체 가져오기  
암호화된 개체를 데이터베이스 프로젝트로 가져올 경우 개체 정의의 전문을 서버에서 항상 검색할 수 있는 것이 아닙니다. 그렇기 때문에 이러한 클래스의 개체를 처리할 때는 가져오기 동작이 다를 수 있습니다.  
  
전문 정의를 검색할 수 없는 경우 개체 머리글/바닥글과 더미 본문이 함께 스크립팅됩니다. 원본이 라이브 데이터베이스이거나 데이터베이스에서 추출한 .dacpac일 때 가져오기를 실행하거나 스키마 비교를 사용하면 이러한 동작이 나타날 수 있습니다.  
  
**더미 본문이 포함된 스크립트**  
  
![더미 본문이 포함된 스크립트](../ssdt/media/ssdt-procwithencryption.gif "더미 본문이 포함된 스크립트")  
  
전체 개체 정의를 사용할 수 있고 검색할 수 있는 경우 가져오기 및 스키마 비교를 실행하면 전체 개체 정의를 프로젝트로 검색할 수 있습니다. 이런 경우는 스크립트, 데이터베이스 프로젝트에서 빌드된 .dacpac 또는 다른 데이터베이스 프로젝트에서 프로젝트를 업데이트할 경우에 해당합니다.  
  
