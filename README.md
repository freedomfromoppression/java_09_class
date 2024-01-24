# java_09_class
package ch09_class;

import java.util.ArrayList;

public class Dictionary {
	// 전역적으로 사용하는 상수
	public static final int OPTION_SUN_NM = 0;
	public static final int OPTION_CODING_WORD = 1;
	public static final int OPTION_RANDOM_ALPH = 2;

	public static ArrayList<String> makeWordList(int option) {
		ArrayList<String> wordList = new ArrayList<>();
		// option 0 학생목록,1 java용어, 2랜덤 알파벳
		if (option == OPTION_SUN_NM) {
			wordList.add("lee apgil");
		} else if (option == OPTION_RANDOM_ALPH) {
			wordList.add("Class");
			wordList.add("public");
			wordList.add("for");
			wordList.add("while");
			wordList.add("method");
		} else if (option == OPTION_RANDOM_ALPH) {
			// 랜덤 알파벳
			String[] alphabet = "qwertyuiopasdfghjklzxcvbnm".split("");
			// 10개만 담기
			for (int i = 0; i < 10; i++) {
				String word = "";
				for (int j = 0; j < 6; j++) {
					int randIdx = (int) (Math.random() * alphabet.length);
					word +=alphabet[randIdx];
				}
				wordList.add(word);
			}
		}
		return wordList;
	}

}
package ch09_class;

import java.util.ArrayList;
import java.util.Collections;

public class FutureMain {

	public static void main(String[] args) {
		ArrayList<FutunreStudent> stuList = new ArrayList<>();
		stuList.add(new FutunreStudent("이앞길", "Lee apgil"));
		stuList.add(new FutunreStudent("강성준", "Kang seongjun"));
		stuList.add(new FutunreStudent("권보성", "Kwon bosung"));
		stuList.add(new FutunreStudent("권유빈", "Kwon yubin"));
		stuList.add(new FutunreStudent("김기찬", "Kim gi chanchan"));
		stuList.add(new FutunreStudent("김대영", "Kim dae young"));
		stuList.add(new FutunreStudent("김동우", "Kim dongwoo"));
		stuList.add(new FutunreStudent("김동현", "Kimdonghyun"));
		stuList.add(new FutunreStudent("김명기", "Kim myeonggi"));
		stuList.add(new FutunreStudent("김영주", "Kim youngju"));
		stuList.add(new FutunreStudent("김유정", "Kimyujeong"));
		stuList.add(new FutunreStudent("김은혜", "Kim eunhye"));
		stuList.add(new FutunreStudent("김휘건", "Kim whgiun"));
		stuList.add(new FutunreStudent("나항진", "Na HangJin"));
		stuList.add(new FutunreStudent("문성민", "Moon Seongmin"));
		stuList.add(new FutunreStudent("박진기", "Park jingi"));
		stuList.add(new FutunreStudent("백현진", "Back hyeonjin"));
		stuList.add(new FutunreStudent("오정연", "Oh jeong yeon"));
		stuList.add(new FutunreStudent("유하영", "Yoo hayoung"));
		stuList.add(new FutunreStudent("이예진", "Lee yejin"));
		stuList.add(new FutunreStudent("이용빈", "Leeyongbin"));
		stuList.add(new FutunreStudent("정유진", "Jung Yujin"));
		System.out.println("=============미래융합교육원 4기 시작===========");
		for (FutunreStudent stu : stuList) {
		}
		for (int i = 0; i < 10; i++) {
			System.out.println((i + 1) + "일차 ==========");
			for (FutunreStudent stu : stuList) {
				stu.endDay();
			}
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
		// leve1기준 내림차순 정렬
//		Collections.sort(stuList, (stuA, stuB) -> stuB.getLeve1() - stuA.getLeve1());
		//Leve1 내림차순, exp 내림차순
		Collections.sort(stuList, (stuA, stuB)->{
			int leve1compare = stuB.getLeve1() -stuA.getLeve1();
			if(leve1compare !=0) {
				return leve1compare;
			}
			//leve1이 같다면, exp에 대해 비교
			return stuB.getExp() - stuA.getExp();
		});
		// Collections.sort 메서드는 두 가지 파라미터를 받음
		// 여기에서 (stuA, stuB)두 학생 객체를 비교
		// stuB.getleve1() - stuA.getleve1() stuB학생과 stuA학생의 값이
		// 양수이면 stuB가 stuA보다 높은 레벨로 간주됨 리스트에서 stuB가 stuA 보다 앞에 위치됨.
		// 만약 stuA - stuB라면 오름차순으로 정렬됨.
		for (int i=0; i<stuList.size(); i++) {
			System.out.println((i+1)+ "등." + stuList.get(i));
		}
	}
}
package ch09_class;

import java.io.StreamCorruptedException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Scanner;

public class QuizMain {

	public static void main(String[] args) {
		//외부에서 new 할 수 없고
		//내부에서 생성되어지 하나의 인스턴스만을 사용
		MovieDB movieDB1 = MovieDB.getInstance();
		MovieDB movieDB2 = MovieDB.getInstance(); // 1,2 같은 인스턴스임
		
		// movieList는 매서드는 가져온 인스턴스로만 호출가능
		ArrayList<Movie> movieList = movieDB1.getMovieList();
		//영화 맞추기
		//명대사 출력
		//2.못맞추면 배우 출력
		//3.못맞추면 초성 출력
		//못맞추면 다음 영화로 넘어감
		Collections.shuffle(movieList); //랜덤으로 섞음.
		int score = 0;
		Scanner scan = new Scanner(System.in);
		for(int i=0; i<movieList.size(); i++) {
			System.out.println(movieList.get(i).getQuotes());
			System.out.print(">>>");
			String answer = scan.nextLine();
			if(answer.equals(movieList.get(i).getTittle())){
				System.out.println("정답입니다.");
			    score +=3;
			    continue;
			}
			System.out.println(movieList.get(i).getActors());
			System.out.print(">>>");
			answer = scan.nextLine();
			if(answer.equals(movieList.get(i).getTittle())){
		       System.out.println("정답입니다.");
		        score +=2;
	           continue;
		}
			System.out.println(movieList.get(i).getWord());
			System.out.print(">>>");
			answer = scan.nextLine();
			if(answer.equals(movieList.get(i).getTittle())){
				System.out.println("정답입니다.");
				score +=2;
				continue;
			
			
			}
		
}
}
}
package ch09_class;

import java.util.ArrayList;
import java.util.Scanner;

public class TypinMain {

	public static void main(String[] args) {
		int num;
		if (args.length > 0) {
			num = Integer.parseInt(args[0]);
		} else {
			num = Dictionary.OPTION_RANDOM_ALPH;// 클래스의 전역상수 (클래스명.상수명)
		}
		Scanner scan = new Scanner(System.in);
		ArrayList<String> wordList = Dictionary.makeWordList(num); // class static method
		long before = System.currentTimeMillis(); // UTC 기준시 부터 지금까지 밀리초
		while (true) {
			int randIdx = (int) (Math.random() * wordList.size());
			// 단어 배열에서 랜덤하게 단어출력
			System.out.println(wordList.get(randIdx));
			System.out.print(">>>");
			String input = scan.nextLine();
			// 문제 단어와 입력단어가 일치하면 삭제
			if (wordList.get(randIdx).equals(input)) {
				wordList.remove(randIdx);
			}
			// 단어가 없으면 종료
			if (wordList.size() == 0) {
				break;
			}
		}
		long after = System.currentTimeMillis();
		long diff = after - before;
		double result = diff / 1000.0; // 초로변경
		System.out.println(result + "초 걸리셨습니다.");

	}

}
