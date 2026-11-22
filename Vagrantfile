ENV["VAGRANT_DEFAULT_PROVIDER"] = "docker"

Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define "db" do |db|
    db.vm.provider "docker" do |d|
      d.image = "postgres:16-alpine"
      d.name = "db-19"
      d.env = {
        "POSTGRES_USER" => "appuser",
        "POSTGRES_PASSWORD" => "pass-19",
        "POSTGRES_DB" => "appdb"
      }
      d.create_args = ["--network=devnet-19", "-v", "pgdata-19:/var/lib/postgresql/data"]
    end
  end

  config.vm.define "web" do |web|
    web.vm.provider "docker" do |d|
      d.image = "lab5-19:1.0"
      d.name = "web-19"
      d.ports = ["8719:5000"]
      d.env = {
        "GREETING" => "Hello",
        "STUDENT" => "Esimova",
        "VARIANT" => "19",
        "DB_HOST" => "db-19",
        "DB_NAME" => "appdb",
        "DB_USER" => "appuser",
        "DB_PASSWORD" => "pass-19"
      }
      d.create_args = ["--network=devnet-19"]
    end
  end
end
