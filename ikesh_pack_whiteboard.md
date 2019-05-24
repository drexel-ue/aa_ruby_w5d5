## Monkey Patching
### my_flatten

Write a method that flattens an array to the specified level. If no level
is specified, it should entirely flatten nested arrays.

Examples:

```ruby
# Without an argument:
[["a"], "b", ["c", "d", ["e"]]].my_flatten = ["a", "b", "c", "d", "e"]

# When given 1 as an argument:
# (Flattens the first level of nested arrays but no deeper)
[["a"], "b", ["c", "d", ["e"]]].my_flatten(1) = ["a", "b", "c", "d", ["e"]]





### Merge Sort

Write a new `Array#merge_sort` method that takes in a proc; it should not modify the array it is called on, but create a new sorted array.

class Array

    def self.merge(left, right, &prc)

        merged_arr = []

        until left.empty? || right.empty?
            case prc.call(left, right)
                when -1
                    merged_arr << left.shift
                when 0
                    merged_arr << left.shift
                when 1
                    merged_arr << right.shift
            end
        end

        merged_arr + left + right

    end

    def merge_sort(&prc)
        prc ||= Proc.new { |a, b| a <=> b }

        midpoint = self.length / 2
        left = self.take(midpoint)
        right = self.drop(midpoint)

        Array.merge(left.merg_sort(prc) right.merg_sort(prc), prc)

    end

    def my_flatten(level = nil)
        duped = self.dup

        return dupe if level == 0

        next_level = level ? level - 1 : nil

        each_with_index do |el, i|
            duped[i..i] = el.my_flatten(next_level) if el.is_a?(Array)
        end

        duped
    end

    ### my_reduce

# Write an array method that calls the given block on each element and
# combines each result one-by-one with a given accumulator. If no accumulator is given, the first element is used.

    def my_reduce(accumulator = nil, &prc)
        if accumulator == nil
            accumulator = self[0]
            (1...length).each do |index|
                accumulator = prc.call(accumulator, self[i])
            end
        else
            (0...length).each do |index|
                accumulator = prc.call(accumulator, self[i])
            end
        end

        accumulator

    end

    # Attempt

    # def my_flatten(level = nil)
    #     return [self[0]] if length == 1 && !self[0].is_a?(Array)

    #     flattened = []
        
    #     if !level.nil?
    #         while level > 0
    #             (0...length).each do |index|
    #                 if self[index].is_a?(Array)
    #                     flattened << self[index].my_flatten(level - 1)
    #                 else
    #                     flattened << self[i]
    #                 end
    #             end

    #         end
    #     else
    #         until !self.any? { |el| el.is_a?(Array) }
    #             (0...length).each do |index|
    #                 if self[index].is_a?(Array)
    #                     flattened << self[index].my_flatten(level - 1)
    #                 else
    #                     flattened << self[i]
    #                 end
    #             end
    #         end
    #     end

    #     flattened
    # end



end


### Shuffled Sentences

# This method returns true if the words in the string can be rearranged to form the
# sentence passed as an argument. Words are separated by spaces.

# Example:

# ```ruby
# "cats are cool".shuffled_sentence_detector("dogs are cool") => false
# "cool cats are".shuffled_sentence_detector("cats are cool") => true

class String
    def shuffled_sentence_detector(sentence)
        return false if self.split(' ').uniq.count < sentence.split(' ').uniq.count
        self_hash = Hash.new { |hash, key| hash[key] = 0 }
        sentence_hash = Hash.new { |hash, key| hash[key] = 0 }
        split(' ').each { |word| self_hash[word] += 1 }
        self_hash == sentence_hash
    end
end


## Recursion

### Fibonacci

# Write a method that finds the first `n` Fibonacci numbers recursively.

def rec_fib(n)
    return [0] if n == 1
    return [0,1] if n == 2
    return [0,1,1] if n == 3

    fibs = rec_fib(n - 1)
    fibs << fibs[-2] + fibs[-1]
    fibs
end
