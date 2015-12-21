require "dotenv/tasks"
require "octokit"

namespace :github do
  desc "Generate end-of-year statistics. Specify the hear with the YEAR environment variable."
  task year: [:dotenv, :setup] do
    year = Integer(ENV.fetch("YEAR"))
    org = ENV.fetch("ORG")
    data = {
      prs: 0,
      comments: 0,
      commits: 0,
    }

    puts "Generating end-of-year statistics for #{org} in #{year}."

    Octokit.org_repos(org).each do |repo|
      full_name = "#{org}/#{repo.name}"
      start = Date.new(year, 1, 1)
      stop = Date.new(year, 12, 31)

      puts "Repo: #{full_name}"
      prs = Octokit.pull_requests(full_name, state: :closed).select do |pr|
        pr.merged_at && pr.merged_at.year == year
      end
      puts "  - PRs: #{prs.size}"

      comments = Octokit.issues_comments(full_name, since: Date.new(year, 1, 1)) do |comment|
        comment.created_at.year == year
      end
      puts "  - Comments: #{comments.size}"

      commits = Octokit.commits_between(full_name, start, stop)
      puts "  - Commits: #{commits.size}"

      data[:prs] += prs.size
      data[:comments] += comments.size
      data[:commits] += commits.size
    end

    puts "TOTAL:"
    puts "  - PRs: #{data[:prs]}"
    puts "  - Comments: #{data[:comments]}"
    puts "  - Commits: #{data[:commits]}"
  end

  task :setup do
    puts "Setting things up..."
    Octokit.configure do |config|
      config.access_token = ENV.fetch("GITHUB_TOKEN")
      config.auto_paginate = true
    end
  end
end

