---
title: 렌더링 확장 프로그램 제거 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 37
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c8ad34be5d818d70b8c46d82dbf348b9d0814824
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080139"
---
# <a name="removing-a-rendering-extension"></a>렌더링 확장 프로그램 제거
  제거 하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 렌더링 확장 프로그램을 제거 하면는 `Extension` 요소에 있는 rsreportserver.config 파일에서 렌더링 확장 프로그램에 대 한 **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< 인스턴스 이름 > services\reportserver** 폴더입니다. 보고서 서버 뿐만 아니라 보고서 디자이너에 대 한 항목을 만든 경우 제거는 `Extension` 에서 요소는 [RSReportDesigner 구성 파일](../../report-server/rsreportdesigner-configuration-file.md) 도 합니다. 구성 정보를 제거한 후에는 구성 요소에서 렌더링 확장 프로그램을 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 파일](../../report-server/reporting-services-configuration-files.md)   
 [렌더링 확장 프로그램 구현](implementing-a-rendering-extension.md)   
 [렌더링 확장 프로그램 개요](rendering-extensions-overview.md)   
 [IRenderingExtension 인터페이스 구현](implementing-the-irenderingextension-interface.md)   
 [확장에 대한 보안 고려 사항](../security-considerations-for-extensions.md)   
 [렌더링 확장 프로그램 배포](deploying-a-rendering-extension.md)  
  
  