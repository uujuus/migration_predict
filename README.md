# migration_predict
### 본 과제는 모 기업의 온라인 교육 서비스를 이용하고 있는 유저들의 데이터를 활용하여 학년별
### 구매, 재구매 여부를 파악하고 이를 통해 학년 별 이탈 여부를 예측하는 모델을 개발하는
### 목적으로 작성되었다.

  
활용된 데이터는 다음과 같다.
<br>
● system_id : system 상 id
<br>
● grade_sect_cd : 학년 (1~6학년)
<br>
● mbr_sex_cd : 성별
<br>
● tmon_pchrg_lrn_dcnt : 당월 유료 학습 일 수
<br>
● acmlt_pchrg_lrn_dcnt : 누적 유료 학습 일 수 (성숙도)
<br>
● acmlt_bilclct_amt : 누적 수금액
<br>
● correct_rate_avg : 당월 획득 점수 평균
<br>
● learning_time_avg : 당월 학습 시간 평균
<br>
● media_action_cnt_sum : 미디어 콘텐츠 내 동영상 행동 횟수 (총합)
<br>
● non_video_viewed_cnt_sum : 미디어 콘텐츠 미시청 행동 횟수
<br>
● get_mm_point_sum : 당월 획득 포인트 합 (사용 x)
<br>
● label : 이탈, 미이탈 여부 (0 - 미이탈, 1 - 이탈)
<br>
● re_purch : 구매, 재구매 여부 (False - 신규, True - 재구매)
<br>

  
이 중에서 학년에 해당하는 컬럼인 grade_sect_cd를 1학년은 1, 2학년은 2의 형태로 숫자형
변수로 바꾸는 전처리를 진행하였다.

또한 구매,재구매 여부에 해당하는 re_purch 컬럼은 boolean 형태이기 때문에 False는 0, True는
1의 형태로 바꾸는 전처리를 하였다.


그래프를 해석한 결과, 저학년일수록 구매 비율이 높은 것을 알 수 있고 고학년으로 올라갈수록
재구매 비율이 높아지는 것을 알 수 있다.
  
다음으로 학년별 Feature importance를 확인하였다.
<br>
1 학년, acc: 0.994, precision: 0.96, recall: 0.6857142857142857, f1:
0.7999999999999999
<br>
2 학년, acc: 0.9935, precision: 0.8, recall: 0.5454545454545454, f1:
0.6486486486486486
<br>
3 학년, acc: 0.9935, precision: 0.7222222222222222, recall: 0.6190476190476191, f1:
0.6666666666666666
<br>
4 학년, acc: 0.9915, precision: 0.7272727272727273, recall: 0.75, f1:
0.7384615384615384
<br>
5 학년, acc: 0.989, precision: 0.7083333333333334, recall: 0.53125,
f1: 0.6071428571428571
<br>
6 학년, acc: 0.985, precision: 0.75, recall: 0.6346153846153846, f1: 0.6875	

   ![image](https://github.com/uujuus/migration_predict/assets/137970651/0f482a80-a68c-42b1-856b-eabfd08c1866)
     
모든 학년이 공통적으로 정확도는 높게 나왔지만 정밀도와 재현율이 상대적으로 낮게
나왔다는 것을 알 수 있다. 그 중에서 재현율이 50%~ 70%의 분포를 보이고 있어 재현율이
특히 떨어지는 것을 알 수 있다. 예를 들면 5학년의 이탈 여부를 예측하는 비율을 보면
실제 이탈하는 학생 중 모델이 이탈했다고 예측한 것의 비율이 53%라는 것이다.
수치상으로 보면 몇몇 학년에 대해서는 신뢰도가 떨어진다고 판단이 된다.
