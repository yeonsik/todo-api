todo-api
========

2013-09-26 (api용 프로젝트 생성 및 환경설정, todo관련파일들 생성)

간단한 todo 어플리케이션을 위한 api 프로젝트입니다.

* api용 프로젝트를 생성하기 위해 먼저 rails-api gem을 설치합니다. 

```
$ gem install rails-api
```

* rails api 프로젝트를 생성합니다. 네이밍을 반드시 _api로 해야되는지는 잘 모르겠네요. 전 https://github.com/rails-api/rails-api 여기보고 최대한 맞춰서 했습니다.

```
$ rails-api new todo_api
```

* 외부로부터 API로 접근할 때 발생하는 Cross Domain 문제를 해결하기 위해서 `rack-cors` 젬을 추가하고 번들 인스톨합니다. 
* (https://github.com/rorlab/vsns-api/blob/master/README.md 참조함)
```
gem 'rack-cors', :require => 'rack/cors'
```

* 그리고 약간의 설정이 필요합니다. (config/application.rb)

```
config.middleware.use Rack::Cors do
  allow do
    origins '*'
    resource '*', :headers => :any, :methods => [:get, :post, :delete, :put, :patch, :options]
  end
end
```

* 여기까지 하면 기본적으로 api를 제공할 수 있는 환경이 맞춰지고 todo api를 제공하기 위해 아래와 같이 합니다.
```
rails-api generate scaffold Item title:string done:boolean
```
```
rake db:migrate
```