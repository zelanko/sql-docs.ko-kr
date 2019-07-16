---
title: 안전 또는 무제한 모드에 대 한 DataFactory 구성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92e3b029d2b18065faf50dcd0343f64b7b01654e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922949"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>안전 또는 무제한 모드에 대한 DataFactory 구성
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 기본적으로 "안전한"를 사용 하 여 ADO 되어 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 구성 합니다. RDS 서버 구성 요소에 대 한 안전 모드는 다음에 해당할 것을 의미 합니다.  
  
1.  처리기는 (레지스트리 키 설정에서 위임 되며)를 업데이트할 필요 합니다.  
  
2.  Msdfmap.handler을 기본 처리기를 등록 하 고, 안전한 처리기 목록에 있는 기본 처리기로 표시 합니다.  
  
3.  Msdfmap.ini 파일이 Windows 디렉터리에 설치 됩니다. RDS를 사용 하 여 3 계층 모드로 전에 필요에 따라이 파일을 구성 해야 합니다.  
  
 필요에 따라 무제한 구성할 수 있습니다 **DataFactory** 설치 합니다. **DataFactory** 사용자 지정 처리기 없이 직접 사용할 수 있습니다. 사용자 연결 문자열을 수정 하 여 사용자 지정 처리기를 사용할 수 있지만 필요 하지 않습니다. 사용의 의미에 대 한 자세한 내용은 합니다 **업데이트할** 개체를 참조 하십시오 [RDS 응용 프로그램 보안](../../../ado/guide/remote-data-service/securing-rds-applications.md)합니다.  
  
 안전 하 게 구성에 대 한 처리기 레지스트리 항목을 설정 하는 레지스트리 파일 handsafe.reg 제공 되었습니다. 안전 모드에서 실행 하려면 handsafe.reg를 실행 합니다.  
  
 Handsafe.reg를 실행 한 후 중지 하 고 명령 프롬프트 창에서 다음 명령을 입력 하 여 웹 서버에서 World Wide Web Publishing 서비스를 다시 시작 해야 합니다. "NET STOP W3SVC" 및 "NET START W3SVC"입니다.  
  
## <a name="see-also"></a>관련 항목  
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)



