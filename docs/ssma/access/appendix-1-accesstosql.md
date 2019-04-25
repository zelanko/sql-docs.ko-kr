---
title: 부록-1 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 521c94fe15c8409377997edfc0b5821f92bed34d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62759639"
---
# <a name="appendix---1-accesstosql"></a>부록-1 (AccessToSQL)
SSMA 콘솔 명령줄 옵션에 대 한 빠른 보기:  
  
|Sl. 아니요.|스위치|필수 여부|스위치 인수|허용 되는 값|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|사용자 계정 컨트롤|scriptfile|올바른 XML 파일 이름입니다.<br /><br />콘솔 스크립트 정의 파일입니다.|  
|2|-v/variable|아니요|variablevaluefile|올바른 XML 파일 이름입니다. 스크립트 파일에서 변수를 사용 하는이 파일을 지정 해야 합니다.|  
|3|-c/serverconnection|아니요|serverconnectionfile|올바른 XML 파일 이름입니다. 이 파일 서버 연결 정보를 포함 합니다.|  
|4|-x/xmloutput|아니요|xmloutputfile|이 옵션은 XML 형식으로 콘솔 출력을 나타냅니다. 이 옵션을 지정 하지 않으면 기본 출력을 텍스트 형식으로 됩니다.<br /><br />Xmloutputfile를 지정 하지 않은 경우 XML 출력은 STDOUT으로 전송 됩니다.<br /><br />Xmloutputfile에는 콘솔 출력은 XML 형식으로 기록 되는 파일의 이름입니다.|  
|5|-l/log|아니요|logfile|유효한 파일 이름입니다.|  
|6|-e/projectenvironment|아니요|projectenvironmentfolder|SSMA 프로젝트 환경 파일이 포함 된 올바른 폴더 이름입니다.|  
|7|-p/securepassword|아니요|-추가 {< server_id > [,... n] &#124; 모든}-c&#124;serverconnection < 서버 연결 파일 > [-v&#124;변수 < 변수 값 파일 >] [-o/덮어쓰기]<br /><br />로 구분하거나 여러<br /><br />-추가 {< server_id > [,... n] &#124; 모든}-s&#124;스크립트 < 스크립트 파일 > [-v&#124;변수 < 변수 값 파일 >] [-o/덮어쓰기]<br /><br />-r/remove {<server_id> [, ...n] &#124; all}<br /><br />-l/list<br /><br />-e/export {<server-id> [, ...n] &#124; all} <encrypted-password -file><br /><br />-i/import {<server-id> [, ...n] &#124; all} <encrypted-password-file>|를 지정 하는 경우이 옵션 다른 옵션과 함께 사용할 수 없습니다.<br /><br />server-id: {문자열} 서버에 대해 제공 된 고유 ID<br /><br />서버 연결 파일: 서버 정의 파일 (serverconnectionfile 또는 scriptfile).<br /><br />variable-value-file: 변수 정의 파일이 하 고 서버 연결 파일에 사용 합니다.<br /><br />암호화 암호-파일: 사용자가 지정한 암호를 사용 하 여 암호화 하는 서버 암호 파일입니다.|  
|8|-?|아니요|해당 사항 없음|해당 사항 없음|  
  
## <a name="see-also"></a>관련 항목  
[SSMA 콘솔 (Access)를 실행합니다.](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
