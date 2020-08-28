---
description: 안전 또는 무제한 모드에 대한 DataFactory 구성
title: 안전 또는 무제한 모드에 대 한 DataFactory 구성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: rothja
ms.author: jroth
ms.openlocfilehash: ab1236205813d1fa3aee0a039703afb10661169c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978364"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>안전 또는 무제한 모드에 대한 DataFactory 구성
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 기본적으로 ADO는 "safe" [RDSServer DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 구성을 사용 하 여 설치 됩니다. RDS 서버 구성 요소에 대 한 안전 모드는 다음을 의미 합니다.  
  
1.  DataFactory에는 처리기가 필요 합니다 (이는 레지스트리 키 설정에 의해 RDSServer).  
  
2.  기본 처리기 msdfmap. 처리기가 등록 되 고, 안전 처리기 목록에 표시 되며, 기본 처리기로 표시 됩니다.  
  
3.  Msdfmap.ini 파일이 Windows 디렉터리에 설치 되어 있습니다. 3 계층 모드로 RDS를 사용 하기 전에 필요에 따라이 파일을 구성 해야 합니다.  
  
 필요에 따라 제한 없는 **DataFactory** 설치를 구성할 수 있습니다. **DataFactory** 은 사용자 지정 처리기 없이 직접 사용할 수 있습니다. 사용자는 연결 문자열을 수정 하 여 사용자 지정 처리기를 계속 사용할 수 있지만 반드시 필요한 것은 아닙니다. **DataFactory** 개체 사용의 의미에 대 한 자세한 내용은 [RDS 응용 프로그램 보안](./securing-rds-applications.md)을 참조 하세요.  
  
 안전 구성에 대 한 처리기 레지스트리 항목을 설정 하기 위해 레지스트리 파일의 수동 safe가 제공 되었습니다. 안전 모드에서 실행 하려면 수동 safe .reg를 실행 합니다.  
  
 직접 safe .reg를 실행 한 후에 명령 프롬프트 창에서 "NET STOP W3SVC" 및 "NET START W3SVC" 명령을 입력 하 여 웹 서버에서 World Wide Web 게시 서비스를 중지 했다가 다시 시작 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DataFactory 사용자 지정](./datafactory-customization.md)   
 [RDS 기본 사항](./rds-fundamentals.md)