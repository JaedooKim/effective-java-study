Java 라이브러리 중에는 close메서드를 호출해 직접 닫아줘야 하는 자원이 많다. InputStream, OutputStream, Connection등이 있다.
자원 닫기는 클라이언트가 놓치기 쉽기 때문에 예측할 수 없는 성능 문제로 이어지기도 한다.

**AutoCloseable**
JDK 1.7 부터 try-with-resources 구문이 추가 되었고, AutoCloseable 인터페이스가 추가되었다. 이 인터페이스가 나오고 부터 Java의 close를 지원하는 클래스에서 AutoCloseable을 구현하도록 변경되었다.

**try-with-resources**
try 절에 AutoCloseable을 구현한 클래스에 대한 인스턴스를 선언하게 되면 try절이 종료되는 시점에 AutoCloseable 인터페이스의 close() 메서드를 자동으로 호출 한다. 그렇기 때문에 이전처럼 finally 구문에서 별도로 자원에 대한 해제를 하지 않아도 된다.

한 때 회사에서 개발하다가, OutputStream 으로 사진을 업로드 하는 메소드에서, 실수로 자원을 닫는 코드를 빼먹었다. 그 결과로 윈도우에서 해당 사진 자원을 계속 붙잡고 있어서 사진이 삭제가 안되는 버그가 있었다. 이처럼 실무에서도 많이 빼먹는 것이 자원 닫기이다. 그러므로 꼭 회수해야 하는 자원을 다룰 때는 try-finally 말고, try-with-resource를 무조건 사용하자. 코드는 더 짧고 분명해지고, 만들어지는 예외 정보도 훨씬 유용하다. try-finally로 작성하면 실용적이지 못할 만큼 코드가 지저분해지지만, try-with-resource로는 정확하고 쉽게 자원을 회수 할 수 있다.