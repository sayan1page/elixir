Installation Steps: ( Platform Ubuntu )

1. Install node js

   sudo apt-get update
   sudo apt-get install nodejs
   sudo apt-get install npm
   sudo apt-get install nodejs-legacy
   exit

2. Install elixir & phoenix

   sudo apt-get update
   wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
   sudo dpkg -i erlang-solutions_1.0_all.deb
   sudo apt-get install esl-erlang
   sudo apt-get install elixir
   exit
   mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez
3. Install postgredb

   sudo apt-get update
   sudo apt-get install postgresql postgresql-contrib
   exit
   sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres';"
   sudo service postgresql restart


4. Deploy the application

    mix phoenix.new crossover_logger_api
    cd crossover_logger_api
    mix ecto.create
    copy the mix.exs file to present directory ( using cp command )
    copy the router.ex file to web/ directory
    copy the app.ex and applog.ex to web/models/ directory
    run command - mix ecto.gen.migration create_app
    a file priv/repo/migrations/**create_app.exs will be created
    cp the content of create_app.exs file to that file. Don't change the file name
    run command - mix ecto.gen.migration create_applog
    a file priv/repo/migrations/**create_applog.exs will be created
    cp the content of create_applog.exs file to that file. Don't change the file name
    mix ecto.migrate
    copy the page_controller.ex to  web/controllers/ folder. replace the old file.
    run  mix deps.get
    run command - mix phoenix.server
    your rest api is ready !!
 
5. Test the application
   
   test register
   curl -XPOST http://localhost:4000/api/v1/register -d '{"display_name":"funapp"}' -H 'content-type: application/json;charset=UTF-8'

   test auth
    curl -XPOST http://localhost:4000/api/v1/auth -H "Authorization: eBa1iWnbKenDvWs5mNyyCYmax0vA_l4j:1GFO0EWLT-d11uqn1odbVgd4k6j2rJ_8"

   test log
    curl -XPOST http://localhost:4000/api/v1/log -H "Authorization:1GFO0EWLT-d11uqn1odbVgd4k6j2rJ_8:1501739673388" -d  '{"log_id":"abcdef","application_id": "Sayan", "logger": "myself","level": "test1", "message": "i am bad"}' -H 'content-type: application/json;charset=UTF-8'

   please not always encode request body in UTF-8 format.




