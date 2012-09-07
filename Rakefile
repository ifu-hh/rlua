require 'bundler/gem_tasks'
require 'rdoc/task'

Rake::RDocTask.new do |rd|
  rd.main        = 'README.rdoc'
  rd.title       = 'RLua Documentation'
  rd.rdoc_files  = Dir['*.rdoc', 'lib/*.rb', 'ext/*.c'].to_a
  rd.rdoc_dir    = 'doc'
  rd.options    += ['--format=hanna']
end

namespace :github do
  task :publish => [:clobber_rdoc, :rdoc] do
    commit = `git rev-parse HEAD`[0..8]
    system <<-END
    set -e

    git clone git@github.com:whitequark/rlua gh-pages
    cd gh-pages

    git checkout gh-pages
    rm * -rf
    cp -r ../doc/* .
    git add -A
    git commit -m "Update pages to match commit #{commit}."

    git push origin gh-pages

    rm gh-pages/ -rf
    END
  end
end