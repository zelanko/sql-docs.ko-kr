---
title: 기타 파일 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio], miscellaneous
- projects [SQL Server Management Studio], files
- solutions [SQL Server Management Studio], files
- miscellaneous files folder [SQL Server]
ms.assetid: 3c952b0b-8f5f-4d86-9e5d-616c10b9df0d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 24a3b22816f33cc204a0809a9f6a38f704baa411
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105264"
---
# <a name="miscellaneous-files"></a>기타 파일
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
프로젝트의 외부에 있는 파일을 ‘기타 파일’이라고 합니다.  솔루션이 열려 있는 경우 프로젝트와 연관된 기타 파일을 열고 수정할 수 있습니다. 파일 확장명이 프로젝트 코드 편집기와 연결되지 않은 경우 파일은 기타 파일로 분류됩니다. 예를 들어 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트 프로젝트에서는 .txt 또는 .mdx 확장명을 가진 파일이 기타 파일로 간주됩니다. MDX 프로젝트에서는 .txt 또는 .sql 확장명을 가진 파일이 기타 파일로 간주됩니다. 파일 확장명을 코드 편집기와 연결하려면 [방법: 파일 확장명을 코드 편집기에 연결](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)을 참조하세요.  
  
기타 파일을 프로젝트에 추가하는 것이 유용한 이유에는 여러 가지가 있습니다. 인식된 스크립트일 필요는 없지만 솔루션 개발에 필수적인 파일이 존재할 수 있습니다. 개발 참고 또는 지침, 데이터 파일, 코드 클립 등을 일반적인 예로 들 수 있습니다.  
  
기타 파일은 유연성을 제공합니다. 예를 들어 데이터베이스에서 테이블과 저장 프로시저를 만들기 위한 여러 스크립트가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트 프로젝트가 있다고 가정해 봅니다. 또한 .BCP 파일 확장명을 가진 테이블에 대한 여러 데이터 파일이 있으며 README.TXT 파일에 실행 지침이 있습니다. 이 경우에 프로젝트 시스템의 소스 제어 및 기타 기능을 활용하기 위해 데이터와 README 파일을 기타 파일로 프로젝트에 추가할 수 있습니다.  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 메뉴와 도구 모음은 열린 파일의 형식에 따라 변경됩니다. 예를 들어 텍스트 파일을 열면 텍스트 편집기 도구 모음이 나타납니다. XML 스키마 파일을 열면 XML 스키마 도구 모음이 나타납니다. XML 스키마를 편집하는 동안 텍스트 편집기 도구 모음을 사용할 수 없습니다. 프로젝트 파일과 기타 파일 간에 전환하면 모든 프로젝트 관련 명령과 도구 모음이 기타 파일과 연관된 명령 및 도구 모음으로 바뀝니다.  
  
## <a name="see-also"></a>참고 항목  
[솔루션 및 프로젝트 관리 파일](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[솔루션&#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[프로젝트&#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
  
